---
title: 重新生成系统数据库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], rebuilding
- REBUILDDATABASE parameter
- rebuilding databases, master
- system databases [SQL Server], rebuilding
ms.assetid: af457ecd-523e-4809-9652-bdf2e81bd876
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b58378e8ba2193a186fb58e3e784bf9bc3cb4d4c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62871264"
---
# <a name="rebuild-system-databases"></a>重新生成系统数据库
  必须重新生成系统数据库来修复[master](master-database.md)、 [model](model-database.md)、 [msdb](msdb-database.md)或[resource](resource-database.md)系统数据库中的损坏问题或者修改默认的服务器级排序规则。 本主题提供如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中重新生成系统数据库的分步说明。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [先决条件](#Prerequisites)  
  
-   **操作**  
  
     [重新生成系统数据库](#RebuildProcedure)  
  
     [重新生成资源数据库](#Resource)  
  
     [创建新的 msdb 数据库](#CreateMSDB)  
  
-   **跟进：**  
  
     [解决重新生成错误](#Troubleshoot)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 重新生成 master、model、msdb 和 tempdb 系统数据库时，将删除这些数据库，然后在其原位置重新创建它们。 如果在重新生成语句中指定了新排序规则，则将使用该排序规则设置创建系统数据库。 用户对这些数据库所做的所有修改都会丢失。 例如，您在 master 数据库中的用户定义对象、msdb 中的预定作业或 model 数据库中对默认数据库设置的更改都会丢失。  
  
###  <a name="Prerequisites"></a>先决条件  
 在重新生成系统数据库之前执行下列任务，以确保可以将系统数据库还原至它们的当前设置。  
  
1.  记录所有服务器范围的配置值。  
  
    ```  
    SELECT * FROM sys.configurations;  
    ```  
  
2.  记录所有应用到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例和当前排序规则的 Service Pack 和修补程序。 重新生成系统数据库后必须重新应用这些更新。  
  
    ```  
    SELECT  
    SERVERPROPERTY('ProductVersion ') AS ProductVersion,  
    SERVERPROPERTY('ProductLevel') AS ProductLevel,  
    SERVERPROPERTY('ResourceVersion') AS ResourceVersion,  
    SERVERPROPERTY('ResourceLastUpdateDateTime') AS ResourceLastUpdateDateTime,  
    SERVERPROPERTY('Collation') AS Collation;  
    ```  
  
3.  记录系统数据库的所有数据文件和日志文件的当前位置。 重新生成系统数据库会将所有系统数据库安装到其原位置。 如果已将系统数据库数据文件或日志文件移动到其他位置，则必须再次移动这些文件。  
  
    ```  
    SELECT name, physical_name AS current_file_location  
    FROM sys.master_files  
    WHERE database_id IN (DB_ID('master'), DB_ID('model'), DB_ID('msdb'), DB_ID('tempdb'));  
    ```  
  
4.  找到 master、model 和 msdb 数据库的当前备份。  
  
5.  如果将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例配置为复制分发服务器，请找到该分发数据库的当前备份。  
  
6.  确保您有重新生成系统数据库的相应权限。 必须是 `sysadmin` 固定服务器角色的成员才能执行此操作。 有关详细信息，请参阅 [服务器级别角色](../security/authentication-access/server-level-roles.md)。  
  
7.  请验证本地服务器上是否有 master、model、msdb 数据模板文件和日志模板文件的副本。 模板文件的默认位置是 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn\Templates。 在重新生成过程中要用到这些文件，而且若想让安装成功这些文件必须存在。 如果缺少这些文件，请运行安装程序的“修复”功能或者手动从安装介质中复制这些文件。 若要在安装介质上查找这些文件，请导航到相应的平台目录（x86 或 x64），然后导航到 setup\sql_engine_core_inst_msi\Pfiles\SqlServr\MSSQL.X\MSSQL\Binn\Templates。  
  
##  <a name="RebuildProcedure"></a>重新生成系统数据库  
 以下过程将重新生成 master、model、msdb 和 tempdb 系统数据库。 无法指定要重新生成哪些系统数据库。 对于群集实例，必须在主动节点上执行此过程，并且在执行此过程之前，必须先使相应群集应用程序组中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源脱机。  
  
 此过程不重新生成 resource 数据库。 请参阅本主题后面的“resource 数据库重新生成过程”部分。  
  
#### <a name="to-rebuild-system-databases-for-an-instance-of-sql-server"></a>重新生成 SQL Server 实例的系统数据库：  
  
1.  将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装介质插入到磁盘驱动器中，或者在本地服务器上，从命令提示符处将目录更改为 setup.exe 文件的位置。 在服务器上的默认位置为 C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Release。  
  
2.  在命令提示符窗口中，输入以下命令。 方括号用来指示可选参数。 不要输入括号。 在使用 Windows 操作系统且启用了用户帐户控制 (UAC) 时，运行安装程序需要提升特权。 必须以管理员身份运行命令提示符。  
  
     `Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName /SQLSYSADMINACCOUNTS=accounts [ /SAPWD= StrongPassword ] [ /SQLCOLLATION=CollationName]`  
  
    |参数名称|说明|  
    |--------------------|-----------------|  
    |/QUIET 或 /Q|指定在没有任何用户界面的情况下运行安装程序。|  
    |/ACTION=REBUILDDATABASE|指定安装程序将重新创建系统数据库。|  
    |/INSTANCENAME =*实例*名称|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的名称。 对于默认实例，请输入 MSSQLSERVER。|  
    |/SQLSYSADMINACCOUNTS=*accounts*|指定要添加到 `sysadmin` 固定服务器角色中的 Windows 组或单个帐户。 指定多个帐户时，请用空格将帐户隔开。 例如，输入 **BUILTIN\Administrators MyDomain\MyUser**。 当您在帐户名称内指定包含空格的帐户时，用双引号将该帐户引起来。 例如，输入 `NT AUTHORITY\SYSTEM`。|  
    |[ /SAPWD=*StrongPassword* ]|指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `sa`帐户的密码。 如果实例使用混合身份验证（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 身份验证）模式，则此参数是必需的。<br /><br /> ** \* \*安全\*说明**该`sa`帐户是一个众所周知的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]帐户，并经常以恶意用户为目标。 因此，为 `sa` 登录名使用强密码非常重要。<br /><br /> 不要为 Windows 身份验证模式指定此参数。|  
    |[ /SQLCOLLATION=*CollationName* ]|指定新的服务器级排序规则。 此参数是可选的。 如果没有指定，则使用服务器的当前排序规则。<br /><br /> ** \* \*重要\*提示**更改服务器级排序规则不会更改现有用户数据库的排序规则。 默认情况下，所有新创建的用户数据库都将使用新排序规则。<br /><br /> 有关详细信息，请参阅 [设置或更改服务器排序规则](../collations/set-or-change-the-server-collation.md)。|  
  
3.  在安装程序完成系统数据库重新生成后，它将返回到命令提示符，而且不显示任何消息。 请检查 Summary.txt 日志文件以验证重新生成过程是否成功完成。 此文件位于 C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Logs。  
  
## <a name="post-rebuild-tasks"></a>重新生成后的任务  
 重新生成数据库后，您可能需要执行以下额外任务：  
  
-   还原 master、model 和 msdb 数据库的最新完整备份。 有关详细信息，请参阅[备份和还原系统数据库 (SQL Server)](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)。  
  
    > [!IMPORTANT]  
    >  如果更改了服务器排序规则，请不要还原系统数据库。 否则，将使新排序规则替换为以前的排序规则设置。  
  
     如果没有备份或者还原的备份不是最新的，请重新创建所有缺失的条目。 例如，重新创建用户数据库、备份设备、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名、端点等缺少的所有条目。 重新创建这些条目的最佳方法是运行创建它们的原始脚本。  
  
> [!IMPORTANT]  
>  建议您保护好脚本，以防未经授权的人员更改脚本。  
  
-   如果将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例配置为复制分发服务器，则必须还原分发数据库。 有关详细信息，请参阅 [备份和还原复制的数据库](../replication/administration/back-up-and-restore-replicated-databases.md)。  
  
-   将系统数据库移到您以前记录的位置。 有关详细信息，请参阅 [Move System Databases](system-databases.md)（移动系统数据库）。  
  
-   验证服务器范围的配置值是否与您以前记录的值相符。  
  
##  <a name="Resource"></a>重新生成资源数据库  
 以下过程将重新生成 resource 系统数据库。 重新生成 resource 数据库时，所有的 Service Pack 和修补程序都将丢失，因此必须重新应用。  
  
#### <a name="to-rebuild-the-resource-system-database"></a>重新生成 resource 系统数据库：  
  
1.  从分发介质中启动 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装程序 (setup.exe)。  
  
2.  在左侧导航区域中单击 **“维护”**，然后单击 **“修复”**。  
  
3.  安装程序支持规则和文件例程将运行，以确保您的系统上安装了必备组件，并且计算机能够通过安装程序验证规则。 单击 **“确定”** 或 **“安装”** 以继续操作。  
  
4.  在“选择实例”页上，选择要修复的实例，然后单击 **“下一步”**。  
  
5.  将运行修复规则以验证修复操作。 若要继续，请单击 **“下一步”** 。  
  
6.  在 **“准备修复”** 页上，单击 **“修复”**。 “完成”页指示修复操作已完成。  
  
##  <a name="CreateMSDB"></a>创建新的 msdb 数据库  
 如果`msdb`数据库已损坏，并且没有`msdb`数据库的备份，则可以使用`msdb` **instmsdb**脚本创建新的。  
  
> [!WARNING]  
>  使用 instmsdb `msdb`脚本重新生成**** 数据库将消除中`msdb`存储的所有信息，例如作业、警报、运算符、维护计划、备份历史记录、基于策略的管理设置、数据库邮件、性能数据仓库等。  
  
1.  停止与 [!INCLUDE[ssDE](../../includes/ssde-md.md)]连接的所有服务，包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理、 [!INCLUDE[ssRS](../../includes/ssrs.md)]、 [!INCLUDE[ssIS](../../includes/ssis-md.md)]以及将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用作数据存储区的所有应用程序。  
  
2.  使用以下命令从命令行启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ： `NET START MSSQLSERVER /T3608`  
  
     有关详细信息，请参阅 [启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)。  
  
3.  在另一个命令行窗口中， `msdb`通过执行以下命令分离数据库，并将* \<servername>* 替换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以下实例：`SQLCMD -E -S<servername> -dmaster -Q"EXEC sp_detach_db msdb"`  
  
4.  使用 Windows 资源管理器，重`msdb`命名数据库文件。 默认情况下，这些文件位于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 DATA 子文件夹中。  
  
5.  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器，停止然后正常重新启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务。  
  
6.  在命令行窗口中，连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并执行以下命令： `SQLCMD -E -S<servername> -i"C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Install\instmsdb.sql" -o" C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Install\instmsdb.out"`  
  
     将* \<servername>* 替换为的[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的文件系统路径。  
  
7.  使用 Windows 记事本，打开 **instmsdb.out** 文件，然后检查输出中是否存在任何错误。  
  
8.  重新应用在该实例上安装的任何 service pack 或修补程序。  
  
9. 重新创建存储在`msdb`数据库中的用户内容，例如作业、警报等。  
  
10. 备份 `msdb` 数据库。  
  
##  <a name="Troubleshoot"></a>解决重新生成错误  
 语法和其他运行时错误会显示在命令提示符窗口中。 检查 Setup 语句中是否存在以下语法错误：  
  
-   每个参数名称前面缺少斜杠标记 (/)。  
  
-   参数名称和参数值之间缺少等号 (=)。  
  
-   参数名称和等号之间存在空格。  
  
-   存在逗号 (,) 或语法中未指定的其他字符。  
  
 重新生成操作完成后，请检查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日志中是否存在任何错误。 默认的日志位置是 C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Logs。 若要查找包含重新生成过程的结果的日志文件，请从命令提示符处将目录更改到“Logs”文件夹，然后运行 `findstr /s RebuildDatabase summary*.*`。 此搜索将引导您找到包含系统数据库重新生成结果的所有日志文件。 打开日志文件，检查其中有无相关错误消息。  
  
## <a name="see-also"></a>另请参阅  
 [系统数据库](system-databases.md)  
  
  
