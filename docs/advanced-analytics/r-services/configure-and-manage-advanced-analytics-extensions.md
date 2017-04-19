---
title: "配置和管理高级分析扩展 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8b00cd155d9ec1ea4a672f2b62ff6bb3e13010a4
ms.lasthandoff: 04/11/2017

---
# <a name="configure-and-manage-advanced-analytics-extensions"></a>配置和管理高级分析扩展
  在安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]后，你可以对 R 运行时以及与 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 相关的其他服务进行轻微的配置更改。  
  
  
 **本主题内容**  
  
-   [预配 SQL Server R Services 的用户帐户](#bkmk_Provisioning)  
  
-   [管理 R 进程使用的内存](#bkmk_ManagingMemory)  
  
-   [使用配置文件更改服务默认值](#bkmk_ChangingConfig) 

-   [修改启动板服务帐户](#bkmk_Launchpad) 
  
##  <a name="bkmk_Provisioning"></a> 预配 SQL Server R Services 的用户帐户  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 R 运行时进程在低特权本地用户帐户的上下文中运行。 在单独的低特权帐户中运行 R 运行时进程具有以下优点：  
  
-   降低在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上运行的 R 运行时进程的特权  
  
-   在 R 运行时会话之间提供隔离  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中执行安装期间，会创建一个新的 Windows 用户帐户池，其中包含运行 R 运行时进程所需的本地用户帐户。 如果需要，你可以修改用来支持 R 的用户数。你的数据库管理员还必须向此组授予权限，以使其可以连接到启用了 R Services 的任何实例。 有关详细信息，请参阅 [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)相关的其他服务进行轻微的配置更改。  
  
 不过，可以针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上的敏感资源定义访问控制列表 (ACL) 来拒绝此组的访问，以防止 R 运行时进程访问资源。  
  
-   用户帐户池链接到一个特定的实例。  对于启用了 R 脚本的每个实例，都会创建一个单独的辅助角色帐户池。 帐户不能在各个实例之间共享。
  
-   池中的用户帐户名采用 SQLInstanceName*nn*格式。 例如，如果你使用默认实例作为 R 服务器，则用户帐户池将支持 MSSQLSERVER01、MSSQLSERVER02 等用户名。  
  
-   用户帐户池的大小是静态的，默认值为 20。 可同时启动的 R 运行时会话数受此用户帐户池的大小限制。 不过，管理员可以使用 SQL Server 配置管理器更改此限制。  
  
  
 有关如何更改用户帐户池的详细信息，请参阅 [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。  
  
##  <a name="bkmk_ManagingMemory"></a> 管理 R 进程使用的内存  
 默认情况下，与 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 关联的 R 运行时进程使用的内存量限制为不超过总计算机内存的 20%。 但是，管理员可根据需要提高此限制。  
  
 通常，对于繁重的 R 任务（例如训练模型或者基于大量数据行进行预测），此数量不够用。 你可能需要降低为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（或其他服务）保留的内存量并使用资源调控器定义一个或多个外部资源池并进行分配。 有关详细信息，请参阅 [R Services 的资源调控器](../../advanced-analytics/r-services/resource-governance-for-r-services.md)。  
  
##  <a name="bkmk_ChangingConfig"></a> 使用配置文件更改高级服务选项  
 
你可以通过编辑 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 配置文件来控制 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的一些高级属性。 此文件是在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 期间创建的，默认情况下以纯文本文件的形式保存在以下位置：  
 
```  
<instance path>\binn\rlauncher.config  
```  
  
 你必须是运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机上的管理员才能对此文件进行更改。 如果你要编辑该文件，我们建议你在保存更改之前创建备份副本。  
  
 例如，若要使用记事本打开默认实例 (MSSQLSERVER) 的配置文件，请以管理员身份打开命令提示符，然后键入以下命令：  
  
```  
C:\>Notepad.exe "%programfiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\binn\rlauncher.config"  
  
```  
  
###  <a name="bkmk_properties"></a> Configuration Properties  
 所有设置采用键-值对的格式，每项设置单独占用一行。 例如，以下属性指定 rlauncher 的跟踪级别：  
  
 Default: TRACE_LEVEL=4  
  
 下表列出了 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持的每项设置及其允许值。  
  
|设置名称|值类型|默认|说明|  
|------------------|----------------|-------------|-----------------|  
|JOB_CLEANUP_ON_EXIT|Integer<br /><br /> 0 = 禁用<br /><br /> 1 = 启用|1<br /><br /> 退出时删除日志文件|指定在完成 R 会话之后，是否应该清除为每个 R 会话创建的临时工作文件夹。 此设置有助于调试。<br /><br /> 注意：这只是一项内部设置 – 请不要更改此值。|  
|TRACE_LEVEL|Integer<br /><br /> 1 = 错误<br /><br /> 2 = 性能<br /><br /> 3 = 警告<br /><br /> 4 = 信息|1<br /><br /> 仅输出警告|配置 R 启动器 (MSSQLLAUNCHPAD) 的跟踪详细程度以进行调试。 此设置将影响存储在以下跟踪文件中的跟踪的详细程度，这两项跟踪均位于 LOG_DIRECTORY 设置指定的路径中：<br /><br /> **rlauncher.log**：针对 T-SQL 查询启动的 R 会话生成的跟踪文件。<br /><br /> 有关此情况的详细信息，请参阅 [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)。|  

## <a name="bkmk_Launchpad"></a>修改启动板服务帐户

对于你在其上配置了 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 的每个实例，都会创建一项单独的 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务。 

默认情况下，启动板配置为使用帐户 NT Service\MSSQLLaunchpad 运行，该帐户预配有运行 R 脚本所需的所有权限。 不过，如果你更改了此帐户，则启动板可能无法启动或者无法访问应当在其中运行 R 脚本的 SQL Server 实例。
 
  如果你修改了服务帐户，请务必使用**本地安全策略**应用程序并更新每个服务帐户的权限以包括以下权限：
  + 调整进程的内存配额 (SeIncreaseQuotaPrivilege)
  + 跳过遍历检查 (SeChangeNotifyPrivilege)
  + 以服务身份登录 (SeServiceLogonRight)
  + 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)

若要深入了解运行 SQL Server 服务所需的权限，请参阅[配置 Windows 服务帐户和权限](https://msdn.microsoft.com/library/ms143504.aspx#Windows)。
   
## <a name="see-also"></a>另请参阅  
 [SQL Server R 服务入门](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  

