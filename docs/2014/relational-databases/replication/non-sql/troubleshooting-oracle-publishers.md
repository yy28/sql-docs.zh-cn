---
title: 对 Oracle 发布服务器进行故障排除 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], Oracle publishing
ms.assetid: be94f1c1-816b-4b1d-83f6-2fd6f5807ab7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c84bf2d98440ff9425cd26a4a71667abea2904e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63021910"
---
# <a name="troubleshooting-oracle-publishers"></a>对 Oracle 发布服务器进行故障排除
  本主题列出配置和使用 Oracle 发布服务器时可能会引发的一系列问题。  
  
## <a name="an-error-is-raised-regarding-oracle-client-and-networking-software"></a>引发关于 Oracle 客户端和网络软件的错误  
 用来在分发服务器上运行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的帐户必须具有对 Oracle 客户端网络软件安装目录（以及所有子目录）的读取和执行权限。 如果未授予权限或者未正确安装 Oracle 客户端组件，您将接收到下列错误消息：  
  
 “用 [Microsoft OLE DB Provider for Oracle] 与服务器连接失败。 找不到 Oracle 客户端和网络组件。 这些组件由 Oracle 公司提供，属于 Oracle 7.3.3 版本或更高版本的客户端软件安装。 访问接口在安装这些组件前无法运行。”  
  
 如果已在分发服务器中安装了 Oracle 客户端，则请确保在完成客户端安装后已将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 停止并重新启动。 这样要求是为了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以识别客户端组件。  
  
 如果已验证授予了这些权限并正确安装组件，但依然存在此错误，请验证 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDTC\MTxOCI 处的注册表设置是否正确：  
  
-   对于 Oracle 10g，正确设置为  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql10.dll  
  
    -   OracleXaLib = oraclient10.dll  
  
-   对于 Oracle 9i，正确设置为  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql9.dll  
  
    -   OracleXaLib = oraclient9.dll  
  
## <a name="the-sql-server-distributor-cannot-connect-to-the-oracle-database-instance"></a>SQL Server 分发服务器无法连接到 Oracle 数据库实例  
 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器无法连接到 Oracle 发布服务器，请确保：  
  
-   分发服务器上已安装必要的 Oracle 软件。  
  
-   Oracle 数据库已联机，可用 SQL*Plus 之类的工具与其连接。  
  
-   复制操作用以连接到 Oracle 发布服务器的登录名具有足够权限。 有关详细信息，请参阅[配置 Oracle 发布服务器](configure-an-oracle-publisher.md)。  
  
-   Oracle 发布服务器配置过程中定义的 TNS 名称显示在 tnsnames.ora 文件中。  
  
-   已使用正确的 Oracle 主目录和路径。 即使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器上只安装了一组 Oracle 二进制文件，也要确保正确设置与 Oracle 主目录相关的环境变量。 如果更改了环境变量值，必须停止并重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 才能使更改生效。  
  
 有关配置和测试连接的详细信息，请参阅[配置 Oracle 发布服务器](configure-an-oracle-publisher.md)中的“在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器上安装和配置 Oracle 客户端网络软件”。  
  
## <a name="the-oracle-publisher-is-associated-with-another-distributor"></a>Oracle 发布服务器与另一分发服务器相关联  
 一个 Oracle 发布服务器只能与一个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器相关联。 如果有不同的分发服务器与 Oracle 发布服务器相关联，则必须先删除它才能使用另一分发服务器。 如果未先删除该分发服务器，就会收到以下错误消息之一：  
  
-   “Oracle 服务器实例‘\<*OraclePublisherName*>'’以前配置为将‘\<*SQLServerDistributorName*>’作为其分发服务器。 若要开始使用‘\<*NewSQLServerDistributorName*>’作为其分发服务器，必须删除 Oracle 服务器实例上的当前复制配置，而这将删除该服务器实例上的所有发布。”  
  
-   “Oracle 服务器‘\<*OracleServerName*>’已被定义为分发服务器‘\<*SQLServerDistributorName*>. *\<DistributionDatabaseName>* ’上的发布服务器‘\<*OraclePublisherName*>’。 请删除此发布服务器或删除公共同义词‘ *\<SynonymName>* ’，以便重新创建。”  
  
 删除 Oracle 发布服务器时，会自动清除 Oracle 数据库中的复制对象。 但是，在某些情况下需要手动清除 Oracle 复制对象。 手动清除复制创建的 Oracle 复制对象：  
  
1.  用 DBA 权限连接到 Oracle 发布服务器。  
  
2.  发出 SQL 命令 `DROP PUBLIC SYNONYM MSSQLSERVERDISTRIBUTOR;`。  
  
3.  发出 SQL 命令 `DROP USER <replication_administrative_user_schema>``CASCADE;`。  
  
## <a name="sql-server-error-21663-is-raised-regarding-the-lack-of-a-primary-key"></a>引发关于缺少主键的 SQL Server 错误 21663  
 事务发布中的项目必须具备有效的主键。 如果它们不具备有效的主键，则在尝试添加项目时会收到以下错误消息：  
  
 “找不到源表 [\<*TableOwner*>].[\<*TableName*>] 的有效主键。”  
  
 有关主键要求的信息，请参阅主题 [Design Considerations and Limitations for Oracle Publishers](design-considerations-and-limitations-for-oracle-publishers.md)中的“唯一索引和约束”部分。  
  
## <a name="sql-server-error-21642-is-raised-regarding-a-duplicate-linked-server-login"></a>引发关于重复链接服务器登录名的 SQL Server 错误 21642  
 在初始配置 Oracle 发布服务器时，会为发布服务器和分发服务器之间的连接创建一个链接服务器项。 该链接服务器的名称与 Oracle TNS 服务名称相同。 如果尝试创建具有相同名称的链接服务器，则会显示以下错误消息：  
  
 “异类发布服务器需要链接服务器。 名为‘ *\<LinkedServerName>* ’的链接服务器已存在。 请删除链接服务器或另选一个发布服务器名称。”  
  
 如果尝试直接创建链接服务器，或者预先删除了 Oracle 发布服务器和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器之间的关系，而当前在尝试重新配置它，就会出现此错误。 如果尝试重新配置发布服务器时收到此错误，请用 [sp_dropserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropserver-transact-sql) 删除链接服务器。  
  
 如果需要通过链接服务器连接来连接到 Oracle 发布服务器，请创建另一个 TNS 服务名称，然后在调用 [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql) 时使用该名称。 有关创建 TNS 服务名称的信息，请参阅 Oracle 文档。  
  
## <a name="sql-server-error-21617-is-raised"></a>引发 SQL Server 错误 21617  
 Oracle 发布操作使用 Oracle 应用程序 SQL*PLUS 将发布服务器支持代码包下载到 Oracle 数据库。 在尝试配置 Oracle 发布服务器之前，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将验证是否可以通过分发服务器上的系统路径来访问 SQL\*PLUS。 如果不能加载 SQL\*PLUS，将显示以下错误消息：  
  
 “无法运行 SQL*PLUS。 请确保分发服务器上安装了最新版本的 Oracle 客户端代码。”  
  
 尝试在分发服务器上找到 SQL\*PLUS。 对于 Oracle 10g 客户端安装，此可执行文件的名称为 sqlplus.exe。 它通常安装在 %ORACLE_HOME%/bin 中。 若要验证 SQL\*PLUS 的路径是否显示在系统路径中，请检查系统变量 **Path** 的值：  
  
1.  右键单击 **“我的电脑”** ，再单击 **“属性”** 。  
  
2.  单击 **“高级”** 选项卡，再单击 **“环境变量”** 。  
  
3.  在 **“环境变量”** 对话框的 **“系统变量”** 列表中，选择 **Path** 变量，然后单击 **“编辑”** 。  
  
4.  在 **“编辑系统变量”** 对话框中：如果 **“变量值”** 文本框中未包含 sqlplus.exe 所在文件夹的路径，请编辑字符串以包含该路径。  
  
5.  在每个打开的对话框中，单击 **“确定”** 退出并保存更改。  
  
 如果在分发服务器上找不到 sqlplus.exe，请在分发服务器上安装最新版本的 Oracle 客户端软件。 有关详细信息，请参阅[配置 Oracle 发布服务器](configure-an-oracle-publisher.md)。  
  
## <a name="sql-server-error-21620-is-raised"></a>引发 SQL Server 错误 21620  
 如果连接到的 Oracle 数据库版本低于 8.1 版，则 Oracle 发布操作要求安装在分发服务器上的 Oracle 客户端软件版本为 9 版或更高版本。 如果连接到的 Oracle 数据库版本是 8.1 版或更高版本，则建议 Oracle 客户端软件版本为 10 版或更高版本。  
  
 尝试配置 Oracle 发布服务器之前，Oracle 发布操作将验证可通过分发服务器上的系统路径访问的 SQL*PLUS 的版本是否为 9 版或更高版本。 如果不是，则显示以下错误消息：  
  
 “通过系统 Path 变量获得的 SQL*PLUS 版本不够新，无法支持 Oracle 发布。 请确保分发服务器上安装了最新版本的 Oracle 客户端代码。”  
  
 如果分发服务器上安装了多个版本的 Oracle 客户端软件，请确保最新版本至少为 9 版，且系统的 Path 变量首先引用此版本（Path 系统变量可以引用其他版本，但最新的版本必须出现在最前面）。 有关编辑系统的 Path 变量的详细信息，请参阅本主题前面的“引发 SQL Server 错误 21617”一节。  
  
## <a name="sql-server-error-21624-or-error-21629-is-raised"></a>引发 SQL Server 错误 21624 或错误 21629  
 对于 64 位分发服务器，Oracle 发布操作使用用于 Oracle 的 Oracle OLEDB 访问接口 (OraOLEDB.Oracle)。 确保分发服务器上安装并注册了 Oracle OLEDB 访问接口。 如果未安装并注册该访问接口，则会显示下列某条错误消息或同时显示这两条错误消息：  
  
-   “在分发服务器 '%s' 上找不到已注册的 Oracle OLEDB 访问接口 OraOLEDB.Oracle。 请确保在分发服务器上安装并注册了最新版本的 Oracle OLEDB 访问接口。”  
  
-   “指示 Oracle 的 Oracle OLEDB 访问接口 OraOLEDB.Oracle 已注册的 CLSID 注册表项不在分发服务器上。 请确保在分发服务器上安装并注册了 Oracle OLEDB 访问接口。”  
  
 如果使用的是 Oracle 客户端软件 10g 版，则访问接口为 OraOLEDB10.dll；如果是 9i 版，则访问接口为 OraOLEDB.dll。 访问接口将安装在 %ORACLE_HOME%\BIN（例如，C:\oracle\product\10.1.0\Client_1\bin）中。 如果确定分发服务器上未安装 Oracle OLEDB 访问接口，则从 Oracle 提供的 Oracle 客户端软件安装光盘上安装它。 有关详细信息，请参阅[配置 Oracle 发布服务器](configure-an-oracle-publisher.md)。  
  
 如果已安装 Oracle OLEDB 访问接口，请确保已将其注册。 若要注册访问接口 DLL，请从安装 DLL 的目录中执行以下命令，然后停止并重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例：  
  
1.  `regsvr32 OraOLEDB10.dll` 或 `regsvr32 OraOLEDB.dll`。  
  
## <a name="sql-server-error-21626-or-error-21627-is-raised"></a>引发 SQL Server 错误 21626 或错误 21627  
 为了验证是否正确配置了 Oracle 发布环境， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 会尝试使用在配置过程中指定的登录凭据连接到 Oracle 发布服务器。 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器不能连接到 Oracle 发布服务器，则会显示以下错误消息：  
  
-   “无法使用 Oracle OLEDB 访问接口 OraOLEDB.Oracle 连接到 Oracle 数据库服务器 '%s'”。  
  
 如果显示此错误消息，请通过使用在 Oracle 发布服务器的配置过程中指定的登录名和密码直接运行 SQL*PLUS，验证与 Oracle 数据库的连接。 有关详细信息，请参阅本主题前面的“SQL Server 分发服务器无法连接到 Oracle 数据库实例”部分。  
  
## <a name="sql-server-error-21628-is-raised"></a>引发 SQL Server 错误 21628  
 对于 64 位分发服务器，Oracle 发布操作使用用于 Oracle 的 Oracle OLEDB 访问接口 (OraOLEDB.Oracle)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将创建注册表项，以允许 Oracle 访问接口与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]一起在进程中运行。 如果读取或写入此注册表项时出现问题，则显示以下错误消息：  
  
 “无法更新分发服务器 '%s'的注册表，以允许 Oracle OLEDB 访问接口 OraOLEDB.Oracle 与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]一起在进程中运行。 请确保当前登录名有权修改 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 拥有的注册表项。”  
  
 Oracle 发布操作要求存在该注册表项，并且对于 64 位分发服务器，它必须设置为 **1** 。 如果该注册表项不存在，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将会尝试创建它。 如果该注册表项存在，但设置为 **0**，则该设置不会改变；Oracle 发布服务器的配置操作将失败。  
  
 查看并修改注册表设置：  
  
1.  单击 **“启动”** ，再单击 **“运行”** 。  
  
2.  在 **“运行”** 对话框中，键入 **regedit**，然后单击 **“确定”** 。  
  
3.  导航到 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\ *\<InstanceName>* \Providers。  
  
     Providers 下应该包含一个名为 OraOLEDB.Oracle 的文件夹。 在此文件夹中应该有一个名为 **AllowInProcess**的 DWORD 值，它的值为 **1**。  
  
4.  如果发现 **AllowInProcess** 被设置为 **0**，请将其更新为 **1**：  
  
    1.  右键单击该注册表项，然后单击 **“修改”** 。  
  
    2.  在 **“编辑字符串”** 对话框的 **“数值数据”** 字段中，键入 **1** 。  
  
## <a name="sql-server-error-21684-is-raised"></a>引发 SQL Server 错误 21684  
 如果管理用户帐户没有足够权限，则会显示以下错误消息：  
  
 “与 Oracle 发布服务器‘%s’管理员登录名关联的权限不足。”  
  
 若要验证授予用户的权限，请执行以下查询： `SELECT * from session_privs`。 输出应与以下内容类似：  
  
 `PRIVILEGE`  
  
 `------------------`  
  
 `CREATE SESSION`  
  
 `CREATE TABLE`  
  
 `CREATE PUBLIC SYNONYM`  
  
 `DROP PUBLIC SYNONYM`  
  
 `CREATE VIEW`  
  
 `CREATE SEQUENCE`  
  
 `CREATE PROCEDURE`  
  
 `CREATE TRIGGER`  
  
## <a name="you-encounter-permissions-issues-for-the-replication-user-schema"></a>遇到复制用户架构的权限问题  
 复制用户架构必须具有[配置 Oracle 发布服务器](configure-an-oracle-publisher.md)中的“手动创建用户架构”所介绍的权限。  
  
## <a name="oracle-error-ora-01000"></a>Oracle 错误 ORA-01000  
 向发布添加项目的过程中，复制在 Oracle 发布服务器上使用游标。 在此过程中，可能会超过发布服务器上可用的最大游标数。 如果出现这种情况，会引发以下错误：  
  
 “ORA-01000: 超过了最大打开游标数”  
  
 若要避免此问题，请确保将 Oracle 数据库中的 **max_open_cursors** 设置设为足够大的数字（至少为 1000）。 有关此设置的详细信息，请参阅 Oracle 文档。  
  
## <a name="oracle-error-ora-01555"></a>Oracle 错误 ORA-01555  
 下列 Oracle 数据库错误与快照复制无关；而与 Oracle 如何构造读取一致数据视图相关：  
  
 "ORA-01555:快照太旧"  
  
 Oracle 使用名为“回滚段”的对象在发出 SQL 语句的时间点处构造读取一致数据视图。 回滚信息被其他并发会话覆盖时，可能出现“快照太旧”错误。 在 Oracle 9i 之前的版本中，推荐使用增加回滚段的大小和/或数量，并将较大事务分配给特定的回滚段来降低此错误的出现频率。  
  
 在 Oracle 9i 中，Oracle 引入了 UNDO 表空间概念，这取代了回滚段。 若要避免 Oracle 9i 中出现“快照太旧”错误，建议您：  
  
-   创建具有适当可用空间量的 UNDO 表空间。  
  
-   对表空间设置保留保证空间（Oracle 10G 及更大）。  
  
-   配置 Oracle 初始化参数 UNDO_MANAGEMENT 和 UNDO_RETENTION。  
  
 有关避免出现“快照太旧”错误的详细信息，请参阅 Oracle 文档。  
  
## <a name="oracle-error-ora-22285"></a>Oracle 错误 ORA-22285  
 如果表包括一个 BFILE 列，则该列的数据会存储于文件系统中。 必须使用以下语法授予复制管理用户帐户对存储数据的目录的访问权限：  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 如果未授予访问权限，日志读取器代理会引发下列错误：  
  
 “ORA-22285: 不存在用于 FILEOPEN 操作的目录或文件”  
  
## <a name="changes-are-made-that-require-reconfiguration-of-the-publisher"></a>进行了需要重新配置发布服务器的更改  
 对复制元数据表或过程的更改需要删除并重新配置发布服务器。 若要重新配置发布服务器，必须用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、Transact-SQL 或 RMO 删除发布服务器并再次配置它。 有关配置发布服务器的信息，请参阅[配置 Oracle 发布服务器](configure-an-oracle-publisher.md)。  
  
 **删除 Oracle 发布服务器 (** SQL Server Management Studio **)**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中连接到 Oracle 发布服务器的分发服务器并展开服务器节点。  
  
2.  右键单击 **“复制”** ，然后单击 **“分发服务器属性”** 。  
  
3.  在 **“分发服务器属性”** 对话框中的 **“发布服务器”** 页上，清除 Oracle 发布服务器的复选框。  
  
4.  单击 **“确定”** 。  
  
 **删除 Oracle 发布服务器 (Transact-SQL)**  
  
-   执行 **sp_dropdistpublisher**。 有关详细信息，请参阅 [sp_dropdistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [配置 Oracle 发布服务器](configure-an-oracle-publisher.md)   
 [Oracle 发布概述](oracle-publishing-overview.md)  
  
  
