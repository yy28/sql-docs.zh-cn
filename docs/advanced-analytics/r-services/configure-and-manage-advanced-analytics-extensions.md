---
title: "配置和管理高级分析扩展 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 20
---
# 配置和管理高级分析扩展
  在安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]后，你可以对 R 运行时以及与 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 相关的其他服务进行轻微的配置更改。  
  
  
 **本主题内容**  
  
-   [预配 SQL Server R Services 的用户帐户](#bkmk_Provisioning)  
  
-   [管理 R 进程使用的内存](#bkmk_ManagingMemory)  
  
-   [使用配置文件更改服务默认值](#bkmk_ChangingConfig) 

-   [修改快速启动板服务帐户](#bkmk_Launchpad) 
  
##  <a name="bkmk_Provisioning"></a> 预配 SQL Server R Services 的用户帐户  
 中的 R 运行时进程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 低特权本地用户帐户的上下文中运行。 在单独的低特权帐户中运行 R 运行时进程具有以下优点：  
  
-   降低在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上运行的 R 运行时进程的特权  
  
-   在 R 运行时会话之间提供隔离  
  
 在安装过程的一部分 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ，新的 Windows *用户帐户池* 创建，其中包含用于运行 R 运行时进程所需的本地用户帐户。 可以修改用户的数，如果需要支持。您的数据库管理员还必须为此组的权限连接到任何已启用了 R 服务的实例。 有关详细信息，请参阅 [对 SQL Server R 服务，请修改用户帐户池](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。  
  
 但是，访问控制列表 (ACL) 可为定义敏感资源上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来拒绝对此组，以防止 R 运行时进程访问的资源访问。  
  
-   用户帐户池链接到的特定实例。  对于每个实例的 R 启用脚本，单独的池的工作人员需要创建帐户。 不能实例之间共享帐户。
  
-   池中的用户帐户名采用 SQLInstanceName*nn*格式。 例如，如果你使用默认实例作为 R 服务器，则用户帐户池将支持 MSSQLSERVER01、MSSQLSERVER02 等用户名。  
  
-   用户帐户池的大小是静态的，默认值为 20。 可同时启动的 R 运行时会话数受此用户帐户池的大小限制。 但是，还可以使用 SQL Server 配置管理器由管理员更改此限制。  
  
  
 有关如何更改用户帐户池的详细信息，请参阅 [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。  
  
##  <a name="bkmk_ManagingMemory"></a> 管理 R 进程使用的内存  
 默认情况下，与 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 关联的 R 运行时进程使用的内存量限制为不超过总计算机内存的 20%。 但是，管理员可根据需要提高此限制。  
  
 通常情况下，此金额将不适用于严重 R 任务，例如定型模型或预测在很多行数据。 您可能需要减少为保留的内存量 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （或其他服务） 和使用资源调控器来定义对外部资源池并分配。 有关详细信息，请参阅 [R 服务的资源调控](../../advanced-analytics/r-services/resource-governance-for-r-services.md)。  
  
##  <a name="bkmk_ChangingConfig"></a> 使用配置文件更改高级服务选项  
 
您可以控制某些高级的属性 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 通过编辑 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 配置文件。 此文件是在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 期间创建的，默认情况下以纯文本文件的形式保存在以下位置：  
 
```  
<instance path>\binn\rlauncher.config  
```  
  
 你必须是运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机上的管理员才能对此文件进行更改。 如果你要编辑该文件，我们建议你在保存更改之前创建备份副本。  
  
 例如，若要使用记事本打开默认实例 (MSSQLSERVER) 的配置文件，请以管理员身份打开命令提示符，然后键入以下命令：  
  
```  
C:\>Notepad.exe "%programfiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\binn\rlauncher.config"  
  
```  
  
###  <a name="bkmk_properties"></a> 配置属性  
 所有设置采用键-值对的格式，每项设置单独占用一行。 例如，以下属性指定 R 进程不能使用 20% 以上的系统内存：  
  
 默认值： `MEMORY_LIMIT_PERCENT=20`  
  
 下表列出了每个支持设置 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ，与允许的值。  
  
|设置名称|值类型|默认|说明|  
|------------------|----------------|-------------|-----------------|  
|JOB_CLEANUP_ON_EXIT|Integer<br /><br /> 0 = 禁用<br /><br /> 1 = 启用|1<br /><br /> 退出时删除日志文件|指定在完成 R 会话之后，是否应该清除为每个 R 会话创建的临时工作文件夹。 此设置有助于调试。<br /><br /> 注意：这只是一项内部设置 – 请不要更改此值。|  
|TRACE_LEVEL|Integer<br /><br /> 1 = 错误<br /><br /> 2 = 性能<br /><br /> 3 = 警告<br /><br /> 4 = 信息|1<br /><br /> 仅输出警告|配置 R 启动器 (MSSQLLAUNCHPAD) 的跟踪详细程度以进行调试。 此设置将影响存储在以下跟踪文件中的跟踪的详细程度，这两项跟踪均位于 LOG_DIRECTORY 设置指定的路径中：<br /><br /> **rlauncher.log**: R 对启动的会话的 T-SQL 查询生成的跟踪文件。<br /><br /> 有关此情况的详细信息，请参阅 [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)。|  

## <a name="bkmk_Launchpad"></a>修改快速启动板服务帐户

单独 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 为在其已配置每个实例创建服务 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]。 

默认情况下，快速启动板配置为使用帐户 NT Service\MSSQLLaunchpad，设置所有必要的权限来运行 R 脚本来运行。 但是，如果您更改此帐户，快速启动板可能无法启动或访问 SQL Server 实例应在何处运行 R 脚本。
 
  如果您修改服务帐户，请务必使用 **本地安全策略** 应用程序和更新每个服务上的权限的帐户包括这些权限︰
  + 调整进程的内存配额 (SeIncreaseQuotaPrivilege)
  + 跳过遍历检查 (SeChangeNotifyPrivilege)
  + 以服务身份登录 (SeServiceLogonRight)
  + 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)

有关运行 SQL Server 服务所需权限的详细信息，请参阅 [配置 Windows 服务帐户和权限](https://msdn.microsoft.com/library/ms143504.aspx#Windows)。
   
## 另请参阅  
 [SQL Server R Services 入门](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  