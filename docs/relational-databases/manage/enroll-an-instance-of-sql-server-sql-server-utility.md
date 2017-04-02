---
title: "注册 SQL Server 的实例（SQL Server 实用工具） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.SWB.makemanaged.agentaccount.F1"
  - "sql13.SWB.makemanaged.welcome.F1"
  - "sql13.SWB.makemanaged.enrolling.F1"
  - "sql13.SWB.makemanaged.instancename.F1"
  - "sql13.SWB.makemanaged.Summary.F1"
  - "sql13.SWB.makemanaged.progress.F1"
  - "sql13.SWB.makemanaged.validation.F1"
helpviewer_keywords: 
  - "注册实例"
ms.assetid: a801c619-611b-4e82-a8d8-d1e01691b7a1
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# 注册 SQL Server 的实例（SQL Server 实用工具）
  将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例注册到现有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中，以便将其性能和配置作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的托管实例进行监视。 实用工具控制点 (UCP) 每隔 15 分钟从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例收集配置和性能信息。 此信息存储在 UCP 上的实用工具管理数据仓库 (UMDW) 中；该 UMDW 文件名是 sysutility_mdw。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 性能数据与策略进行比较，以便帮助标识资源使用瓶颈和整合机会。  
  
 在此版本中，UCP 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有托管实例必须满足以下要求：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必须是 10.50 版或更高版本。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例类型必须是[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具必须在单个 Windows 域或具有双向信任关系的多个域内操作。  
  
-   UCP 和 SQL Server 的所有托管实例上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户必须对 Active Directory 中的用户具有读取权限。  
  
-   要注册的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例不能是 SQL Azure。  
  
 在此版本中，UCP 必须满足以下要求：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例必须是受支持版本。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)。  
  
-   我们建议 UCP 由 SQL Server 的区分大小写的实例承载。  
  
-   对于针对 UCP 计算机的容量计划，请考虑以下建议：  
  
    -   在典型的方案中，UCP 上 UMDW 数据库 (sysutility_mdw) 使用的磁盘空间是每年 SQL Server 的每个托管实例大约 2 GB。 此估计值可能会根据托管实例收集的数据库和系统对象的数目而发生变化。 UMDW (sysutility_mdw) 磁盘空间增长率在最初的两天最高。  
  
    -   在典型的方案中，UCP 上 msdb 使用的磁盘空间是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每个托管实例大约 20 MB。 请注意，此估计值可能会根据资源使用策略以及托管实例收集的数据库和系统对象的数目而发生变化。 一般而言，磁盘空间使用率随着违反策略的数目的增加而增加，并且随着易失性资源的可调时间范围的持续时间长度的增加而增加。  
  
    -   请注意，在某一托管实例的数据保持期到期前，从 UCP 中删除该托管实例将不会降低 UCP 数据库所占用的磁盘空间。  
  
 在此版本中，SQL Server 的所有托管实例必须满足以下要求：  
  
-   我们建议，如果 UCP 由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的不区分大小写的实例承载，则 SQL Server 的托管实例也应是不区分大小写。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具监视不支持 FILESTREAM 数据。  
  
 有关详细信息，请参阅 [SQL Server 的最大容量规范](../../sql-server/maximum-capacity-specifications-for-sql-server.md)和 [SQL Server 2016 各个版本支持的功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)。  
  
 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具概念的详细信息，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
> [!IMPORTANT]  
>  支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具收集组与非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具收集组并行。 也就是说，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的某一托管实例是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的成员时，该托管实例可由其他收集组监视。 但要注意的是，该托管实例上的所有收集组会将其数据上载到实用工具管理数据仓库中。 有关详细信息，请参阅[在 SQL Server 的同一实例中运行实用工具和非实用工具收集组的注意事项](../../relational-databases/manage/run utility and non-utility collection sets on same sql instance.md)和[配置你的实用工具控制点数据仓库（SQL Server 实用工具）](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)。  
  
## 向导步骤  
 以下各节提供与向导工作流中每一页有关的详细信息。 单击链接可以导航到向导中某一页的详细信息。 有关此操作的 PowerShell 脚本的详细信息，请参阅 PowerShell [示例](#PowerShell_enroll)。  
  
-   [注册实例向导简介](#Welcome)  
  
-   [指定 SQL Server 的实例](#Instance_name)  
  
-   [连接对话框](#Connection_dialog)  
  
-   [实用工具收集组帐户](#Proxy_configuration)  
  
-   [SQL Server 实例验证](#Validation_rules)  
  
-   [实例注册摘要](#Summary)  
  
-   [注册 SQL Server 的实例](#Enrolling)  
  
##  <a name="Welcome"></a> 注册实例向导简介  
 若要启动该向导，请展开实用工具控制点上的实用工具资源管理器树，右键单击“托管实例”，然后选择“添加托管实例…”。  
  
 若要继续，请单击 **“下一步”**。  
  
##  <a name="Instance_name"></a> 指定 SQL Server 的实例  
 若要从连接对话框中选择某一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，请单击 **“连接…”**。 以 ComputerName\InstanceName 的格式提供计算机名称和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称。 有关详细信息，请参阅[连接到服务器（数据库引擎）](../../ssms/f1-help/connect-to-server-database-engine.md)。  
  
 若要继续，请单击 **“下一步”**。  
  
##  <a name="Connection_dialog"></a> 连接对话框  
 在“连接到服务器”对话框中，验证服务器类型、计算机名称和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称信息。 有关详细信息，请参阅[连接到服务器（数据库引擎）](../../ssms/f1-help/connect-to-server-database-engine.md)。  
  
> [!NOTE]  
>  如果连接是加密的，则使用加密连接。 如果连接未加密，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具将使用加密连接重新进行连接。  
  
 若要继续，请单击 **“连接…”**。  
  
##  <a name="Proxy_configuration"></a> 实用工具收集组帐户  
 指定要运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具收集组的 Windows 域帐户。 此帐户用作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具收集组的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户。 此外，也可以使用现有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户。 若要满足验证要求，请使用以下准则来指定帐户。  
  
 如果您指定了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户选项：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户必须是 Windows 域帐户，且不是 LocalSystem、NetworkService 或 LocalService 之类的内置帐户。  
  
 若要继续，请单击 **“下一步”**。  
  
##  <a name="Validation_rules"></a> SQL Server 实例验证  
 在此版本中，在要注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上，必须满足以下条件：  
  
|条件|纠正措施|  
|---------------|-----------------------|  
|对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例和 UCP，您必须具有管理员权限。|对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例和 UCP，以具有管理员权限的帐户登录。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本必须支持实例注册。|有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 应启用 TCP/IP。|在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 上启用 TCP/IP。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例已不能向任何其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 注册。|如果您指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例已作为现有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的一部分进行管理，则您无法向其他 UCP 注册它。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例不能已经是 UCP。|如果您指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例已经是与您连接到的 UCP 不同的其他 UCP，则不能在此 UCP 中注册它。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例必须安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具收集组。|重新安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例上的收集组必须停止运行。|停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例上预先存在的收集组。 如果数据收集器被禁用，则启用它，停止正在运行的所有收集组，然后为创建 UCP 操作重新运行验证规则。<br /><br /> 启用数据收集器：<br /><br /> 在对象资源管理器中，展开 **“管理”** 节点。<br /><br /> 右键单击“数据收集”，然后单击“启用数据收集”。<br /><br /> 停止收集组：<br /><br /> 在对象资源管理器中，依次展开“管理”节点、 **“数据收集”**、 **“系统数据收集组”**。<br /><br /> 右键单击要停止的收集组，然后单击“停止数据收集组”。<br /><br /> 出现一个显示此操作结果的消息框，收集组图标上的红色圆圈指示收集组已停止运行。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务必须启动。|在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例上启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理服务。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例，则将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务配置为手动启动。 否则，将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务配置为自动启动。|  
|必须在 UCP 上启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务。|在 UCP 上启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例，则将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务配置为手动启动。 否则，将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务配置为自动启动。|  
|WMI 必须正确配置。|若要排查 WMI 配置问题，请参阅 [SQL Server 实用工具故障排除](../Topic/Troubleshoot%20the%20SQL%20Server%20Utility.md)。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户必须是 UCP 上有效的 Windows 域帐户。|指定一个有效的 Windows 域帐户。 为了确保该帐户是有效帐户，请使用 Windows 域帐户登录到 UCP。|  
|如果您选择代理帐户选项，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户必须是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的指定实例上的有效 Windows 域帐户。|指定一个有效的 Windows 域帐户。 为了确保该帐户是有效帐户，请使用 Windows 域帐户登录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户不能是 Network Service 之类的内置帐户。|重新将该帐户分配到 Windows 域帐户。 为了确保该帐户是有效帐户，请使用 Windows 域帐户登录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户必须是 UCP 上有效的 Windows 域帐户。|指定一个有效的 Windows 域帐户。 为了确保该帐户是有效帐户，请使用 Windows 域帐户登录到 UCP。|  
|如果您选择服务帐户选项，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户必须是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的指定实例上的有效 Windows 域帐户。|指定一个有效的 Windows 域帐户。 为了确保该帐户是有效帐户，请使用 Windows 域帐户登录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例。|  
  
 如果在验证结果中存在失败的条件，则纠正妨碍性问题后单击 **“重新运行验证”** 以便验证计算机配置。  
  
 若要保存验证报表，请单击 **“保存报表”** ，然后指定文件的位置。  
  
 若要继续，请单击 **“下一步”**。  
  
##  <a name="Summary"></a> 实例注册摘要  
 摘要页列出与要添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例有关的信息。  
  
 托管实例设置：  
  
-   SQL Server 实例名称：ComputerName\InstanceName  
  
-   实用工具收集组帐户：DomainName\UserName  
  
 若要继续，请单击 **“下一步”**。  
  
##  <a name="Enrolling"></a> 注册 SQL Server 的实例  
 “注册”页提供操作的状态：  
  
-   准备用于注册的实例。  
  
-   为收集的数据创建缓存目录。  
  
-   配置实用工具收集组。  
  
 若要保存与注册操作有关的报表，请单击 **“保存报表”** ，然后指定文件的位置。  
  
 若要完成向导，请单击 **“完成”**。  
  
> [!NOTE]  
>  如果您使用 SQL Server 身份验证来连接到要注册的 SQL Server 实例，并且指定属于与 UCP 所在的域不同的其他 Active Directory 域的代理帐户，则实例验证将成功，但注册操作将失败并且具有以下错误消息：  
>   
>  执行 Transact-SQL 语句或批处理时发生了异常。 (Microsoft.SqlServer.ConnectionInfo)  
>   
>  其他信息: 无法获取有关 Windows NT 组/用户 '\<DomainName\AccountName>' 的信息，错误代码 0x5。 （Microsoft SQL Server，错误：15404）  
>   
>  有关排除此故障的详细信息，请参阅 [SQL Server 实用工具故障排除](../Topic/Troubleshoot%20the%20SQL%20Server%20Utility.md)。  
  
> [!IMPORTANT]  
>  不要更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例上“实用工具信息”收集组的任何属性，并且不要手动打开或关闭数据收集，因为数据收集由实用工具代理作业控制。  
  
 在完成注册实例向导后，在 SSMS 的 **“实用工具资源管理器导航”** 窗格中单击 **“托管实例”** 节点。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的已注册实例将显示在 **“实用工具资源管理器内容”** 窗格的列表视图中。  
  
 数据收集过程将立即开始，但可能需要最长 30 分钟的时间，数据才会首次出现在实用工具资源管理器内容窗格的面板和视点中。 数据收集将以每 15 分钟一次的频率继续执行。 若要刷新数据，请右键单击“实用工具资源管理器导航”窗格的“托管实例”节点，然后选择“刷新”，或者在列表视图中右键单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称，然后选择“刷新”。  
  
 若要从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中删除托管实例，请在“实用工具资源管理器导航”窗格中选择“托管实例”以便填充托管实例的列表视图，在“实用工具资源管理器内容”列表视图中右键单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称，然后选择“取消实例托管”。  
  
##  <a name="PowerShell_enroll"></a> 使用 PowerShell 注册 SQL Server 的实例  
 使用下面的示例将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例注册到现有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中：  
  
```  
> $UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
> $SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
> $Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($SqlStoreConnection);  
> $Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\ManagedInstanceName";  
> $InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
> $ManagedInstance = $Utility.EnrollInstance($InstanceConnection, "ProxyAccount", "ProxyPassword");  
```  
  
## 另请参阅  
 [SQL Server 实用工具的功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [在 SQL Server 实用工具中监视 SQL Server 的实例](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [SQL Server 实用工具故障排除](../Topic/Troubleshoot%20the%20SQL%20Server%20Utility.md)  
  
  