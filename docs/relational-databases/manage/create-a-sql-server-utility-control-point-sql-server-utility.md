---
title: 创建 SQL Server 实用工具控制点（SQL Server 实用工具）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.SWB.create.ucp.validation.F1
- sql13.SWB.create.ucp.Summary.F1
- sql13.SWB.create.ucp.progress.F1
- sql13.SWB.create.ucp.agentconfiguration.F1
- sql13.SWB.create.ucp.welcome.F1
- sql13.SWB.create.ucp.instancename.F1
helpviewer_keywords:
- Create UCP
- UCP
ms.assetid: d5335124-1625-47ce-b4ac-36078967158c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b342e77c542cd9f3357bccd4b97f3a876d1f5f1d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68115686"
---
# <a name="create-a-sql-server-utility-control-point-sql-server-utility"></a>创建 SQL Server 实用工具控制点（SQL Server 实用工具）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  一个企业可以具有多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具，并且每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具可以管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的多个实例和多个数据层应用程序。 每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具都具有一个且仅有一个实用工具控制点 (UCP)。 必须为每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具分别创建一个新的 UCP。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每个托管实例以及每个数据层应用程序都是一个且只能是一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的成员，并且由单个 UCP 管理。  
  
 UCP 每隔 15 分钟从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例收集配置和性能信息。 此信息存储在 UCP 上的实用工具管理数据仓库 (UMDW) 中；该 UMDW 文件名是 sysutility_mdw。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 性能数据与策略进行比较，以便帮助标识资源使用瓶颈和整合机会。  
  
## <a name="before-you-begin"></a>开始之前  
 创建 UCP 之前，请查看以下要求和建议。  
  
 在此版本中，UCP 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有托管实例必须满足以下要求：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必须是 10.50 版或更高版本。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例类型必须是 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具必须在单个 Windows 域内或跨具有双向信任关系的多个域操作。  
  
-   UCP 和 SQL Server 的所有托管实例上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户必须对 Active Directory 中的用户具有读取权限。  
  
 在此版本中，UCP 必须满足以下要求：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例必须是受支持版本。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
-   我们建议 UCP 由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的区分大小写的实例承载。  
  
 对于针对 UCP 计算机的容量计划，请考虑以下建议：  
  
-   在典型的方案中，UCP 上 UMDW 数据库 (sysutility_mdw) 使用的磁盘空间是每年 SQL Server 的每个托管实例大约 2 GB。 此估计值可能会根据托管实例收集的数据库和系统对象的数目而发生变化。 UMDW (sysutility_mdw) 磁盘空间增长率在最初的两天最高。  
  
-   在典型的方案中，UCP 上 msdb 使用的磁盘空间是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个托管实例大约 20 MB。 请注意，此估计值可能会根据资源使用策略以及托管实例收集的数据库和系统对象的数目而发生变化。 一般而言，磁盘空间使用率随着违反策略的数目的增加而增加，并且随着易失性资源的可调时间范围的持续时间长度的增加而增加。  
  
-   请注意，在某一托管实例的数据保持期到期前，从 UCP 中删除该托管实例将不会降低 UCP 数据库所占用的磁盘空间。  
  
 在此版本中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有托管实例必须满足以下要求：  
  
-   我们建议，如果 UCP 由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的不区分大小写的实例承载，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例也应是不区分大小写。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具监视不支持 FILESTREAM 数据。  
  
 有关详细信息，请参阅 [SQL Server 的最大容量规范](../../sql-server/maximum-capacity-specifications-for-sql-server.md) 和 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
### <a name="remove-previous-utility-control-points-before-installing-a-new-one"></a>在安装新的实用工具控制点之前删除以前的实用工具控制点  
 如果您在某一 SQL Server 实例上安装实用工具控制点 (UCP)，并且该实例曾配置为 UCP，则必须在执行此操作前删除所有 SQL Server 托管实例并且删除该 UCP。 可以通过运行 **sp_sysutility_ucp_remove** 存储过程来执行此操作。  
  
 在运行该过程之前，请注意以下要求：  
  
-   该过程必须在作为 UCP 的计算机上运行。  
  
-   该过程必须由具有 sysadmin 权限的用户运行，创建 UCP 要求同样的权限。  
  
-   SQL Server 的所有托管实例必须都从该 UCP 中删除。 请注意，该 UCP 是 SQL Server 的托管实例。 有关详细信息，请参阅[操作说明：从 SQL Server 实用工具中删除 SQL Server 实例](https://go.microsoft.com/fwlink/?LinkId=169392)。  
  
 使用此过程可以从 SQL Server 实用工具中删除 SQL Server UCP。 在完成该操作后，可以再次在 SQL Server 的实例上创建 UCP。  
  
 使用 SQL Server Management Studio 连接到该 UCP，然后运行以下脚本：  
  
```  
EXEC msdb.dbo.sp_sysutility_ucp_remove;  
```  
  
> [!NOTE]  
>  如果删除了 UCP 的 SQL Server 实例具有非实用工具数据收集组，则该过程将不删除 sysutility_mdw 数据库。 在此情况下，必须首先手动删除 sysutility_mdw 数据库，然后才能再次创建 UCP。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每个托管实例以及每个数据层应用程序都是一个且只能是一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的成员，并且由单个 UCP 管理。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具概念的详细信息，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
 UCP 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的中心原因点。 使用 UCP，你可以查看从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据层应用程序收集的配置和性能信息，并且执行常规的容量规划活动。 UCP 是用于从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具注册和删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的启动点。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中注册 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例后，可以监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例和数据层应用程序的资源运行状况，以便发现合并机会和确定资源瓶颈。 有关详细信息，请参阅 [在 SQL Server 实用工具中监视 SQL Server 的实例](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)。  
  
> [!IMPORTANT]  
>  支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具收集组与非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具收集组并行。 也就是说，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的某一托管实例是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的成员时，该托管实例可由其他收集组监视。 但要注意的是，该托管实例上的所有收集组会将其数据上载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具管理数据仓库中。 有关详细信息，请参阅[在 SQL Server 的同一实例中运行实用工具和非实用工具收集组的注意事项](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)和[配置你的实用工具控制点数据仓库（SQL Server 实用工具）](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)。  
  
## <a name="wizard-steps"></a>向导步骤  
 ![](../../relational-databases/manage/media/create-ucp.gif "Create_UCP")  
  
 以下各节提供与用于创建新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 的向导工作流中每一页有关的详细信息。 要启动向导以创建新的 UCP，则从 SSMS 的“视图”菜单中打开“实用工具资源管理器”窗格，然后单击“实用工具资源管理器”窗格顶部的 ![](../../relational-databases/manage/media/create-ucp.gif "Create_UCP")“创建 UCP”按钮  。  
  
 单击下面列表中的链接可以导航到向导中某一页的详细信息：  
  
 有关此操作的 PowerShell 脚本的详细信息，请参阅 [示例](#PowerShell_create_UCP)。  
  
-   [创建 UCP 向导简介](#Welcome)  
  
-   [指定实例](#Instance_name)  
  
-   [连接对话框](#Connection_dialog)  
  
-   [实用工具收集组帐户](#Agent_configuration)  
  
-   [验证规则](#Validation_rules)  
  
-   [摘要](#Summary)  
  
-   [创建实用工具控制点](#Creating_UCP)  
  
##  <a name="introduction-to-create-ucp-wizard"></a><a name="Welcome"></a> 创建 UCP 向导简介  
 如果您打开实用工具资源管理器并且没有连接的实用工具控制点，则必须连接到一个控制点或创建一个新的控制点。  
  
 连接到现有 UCP - 如果在你的部署中已存在一个实用工具控制点，则可以通过单击“实用工具资源管理器”窗格顶部的 ![](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")“连接到实用工具”按钮连接到该实用工具控制点   。 若要连接到现有 UCP，您必须具有管理员凭据或是实用工具读取者角色的成员。 请注意，每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具只能有一个 UCP，并且只能从 SSMS 的某一实例连接到一个 UCP。  
  
 创建新的 UCP - 要创建新的实用工具控制点，请单击“实用工具资源管理器”窗格顶部的 ![](../../relational-databases/manage/media/create-ucp.gif "Create_UCP")“创建 UCP”按钮   。 若要创建一个新的 UCP，必须指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称并在连接对话框中提供管理员凭据。 请注意，每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具只能有一个 UCP。  
  
##  <a name="specify-instance"></a><a name="Instance_name"></a> 指定实例  
 指定与您正创建的 UCP 有关的以下信息：  
  
-   **实例名称** - 若要从连接对话框中选择某一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，请单击“连接…”  。以 ComputerName\InstanceName 的格式提供计算机名称和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称。  
  
-   **实用程序名称** - 指定将用于在网络上标识 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的名称。  
  
 若要继续，请单击 **“下一步”** 。  
  
##  <a name="connection-dialog"></a><a name="Connection_dialog"></a> 连接对话框  
 在“连接到服务器”对话框中，验证服务器类型、计算机名称和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称信息。 有关详细信息，请参阅[连接到服务器（数据库引擎）](https://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41)。  
  
> [!NOTE]  
>  如果连接是加密的，将使用加密连接。 如果连接未加密，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具将使用加密连接重新进行连接。  
  
 若要继续，请单击“连接...”  。  
  
##  <a name="utility-collection-set-account"></a><a name="Agent_configuration"></a> 实用工具收集组帐户  
 指定要运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具收集组的 Windows 域帐户。 此帐户用作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具收集组的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户。 此外，也可以使用现有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户。 若要满足验证要求，请使用以下准则来指定帐户。  
  
 如果您指定了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户选项：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户必须是 Windows 域帐户，且不是 LocalSystem、NetworkService 或 LocalService 之类的内置帐户。  
  
 若要继续，请单击 **“下一步”** 。  
  
##  <a name="validation-rules"></a><a name="Validation_rules"></a> 验证规则  
 在此版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，在将创建 UCP 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上，必须满足以下条件：  
  
|验证规则|纠正措施|  
|---------------------|-----------------------|  
|对于将创建实用工具控制点的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，您必须具有管理员权限。|在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例上，以具有管理员权限的帐户登录。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本必须是 10.50 版或更高版本。|指定用于承载 UCP 的不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例必须是受支持版本。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。|指定用于承载 UCP 的不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例不得是已向任何其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 注册的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。|指定用于承载 UCP 的不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，或者从当前是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例的 UCP 取消注册该 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例不能已是某一实用工具控制点的宿主。|指定用于承载 UCP 的不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例应启用 TCP/IP。|为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的指定实例启用 TCP/IP。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例不能具有名为“sysutility_mdw”的数据库。|创建 UCP 操作将创建一个名为“sysutility_mdw”的实用工具管理数据仓库 (UMDW)。 该操作要求该名称在验证规则运行时在计算机上不存在。 若要继续，您必须删除或重命名名为“sysutility_mdw”的任何数据库。 有关重命名操作的详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例上的收集组必须停止运行。|在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的指定实例上创建 UCP 时停止预先存在的收集组。 如果数据收集器被禁用，则启用它，停止正在运行的所有收集组，然后为创建 UCP 操作重新运行验证规则。<br /><br /> 启用数据收集器：<br /><br /> 在对象资源管理器中，展开 **“管理”** 节点。<br /><br /> 右键单击 **“数据收集”** ，然后单击 **“启用数据收集”** 。<br /><br /> 停止收集组：<br /><br /> 在对象资源管理器中，依次展开“管理”节点、 **“数据收集”** 、 **“系统数据收集组”** 。<br /><br /> 右键单击要停止的收集组，然后单击 **“停止数据收集组”** 。<br /><br /> 出现一个显示此操作结果的消息框，收集组图标上的红色圆圈指示收集组已停止运行。|  
|指定实例上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务必须启动。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务必须配置为手动启动。 否则， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务必须配置为自动启动。|启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例，则将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务配置为手动启动。 否则，将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务配置为自动启动。|  
|WMI 必须正确配置。|若要排查 WMI 配置问题，请参阅 [SQL Server 实用工具故障排除](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户不能是 Network Service 之类的内置帐户。|如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户是 Network Service 之类的内置帐户，则将该帐户重新分配给作为 sysadmin 的 Windows 域帐户。|  
|如果您选择代理帐户选项，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户必须是有效的 Windows 域帐户。|指定一个有效的 Windows 域帐户。 为了确保该帐户是有效帐户，请使用 Windows 域帐户登录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例。|  
|如果你选择服务帐户选项，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户不能是 Network Service 之类的内置帐户。|如果该 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户是 Network Service 之类的内置帐户，则将该帐户重新分配给 Windows 域帐户。|  
|如果您选择服务帐户选项，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户必须是有效的 Windows 域帐户。|指定一个有效的 Windows 域帐户。 为了确保该帐户是有效帐户，请使用 Windows 域帐户登录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例。|  
  
 如果在验证结果中存在失败的条件，则纠正妨碍性问题后单击 **“重新运行验证”** 以便验证计算机配置。  
  
 若要保存验证报表，请单击 **“保存报表”** ，然后指定文件的位置。  
  
 若要继续，请单击 **“下一步”** 。  
  
##  <a name="summary"></a><a name="Summary"></a>总结  
 摘要页显示您提供的与 UCP 有关的信息：  
  
-   承载该 UCP 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的名称。  
  
-   将用于运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具数据收集作业的帐户的名称。  
  
 若要更改 UCP 配置设置，请单击 **“上一步”** 。 若要继续，请单击 **“下一步”** 。  
  
##  <a name="creating-the-utility-control-point"></a><a name="Creating_UCP"></a> 创建实用工具控制点  
 在创建 UCP 的操作过程中，该向导将显示相关步骤并提供有关状态：  
  
-   正在为创建 UCP 准备 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
-   正在创建实用工具管理数据仓库 (UMDW)。  
  
-   正在初始化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UMDW；UMDW 文件名为 sysutility_mdw。  
  
-   正在配置 UCP。  
  
-   正在配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具收集组。  
  
 若要保存与创建 UCP 操作有关的报表，请单击 **“保存报表”** ，然后指定文件的位置。  
  
 若要完成向导，请单击 **“完成”** 。  
  
 在完成创建 UCP 向导后，对于为“已部署的数据层应用程序”、“托管实例”和“实用工具管理”在其下具有节点的 UCP，SSMS 的实用工具资源管理器导航窗格中将显示一个节点。 该 UCP 将自动成为托管实例。  
  
 数据收集过程将立即开始，但可能需要最长 30 分钟的时间，数据才会首次出现在实用工具资源管理器内容窗格的面板和视点中。 数据收集将以每 15 分钟一次的频率继续执行。 初始数据将来自该 UCP 本身。 也就是说，该 UCP 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的第一个托管实例。  
  
 若要显示面板，请单击 **“视图”** ，然后从 SSMS 菜单中选择 **“实用工具资源管理器内容”** 。 若要刷新数据，请在实用工具资源管理器窗格中右键单击实用工具名称，然后选择“刷新”  。  
  
 有关如何将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的其他实例注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中的详细信息，请参阅[注册 SQL Server 实例（SQL Server 实用工具）](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)。 若要从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中将该 UCP 作为托管实例删除，请在“实用工具资源管理器”  窗格中选择“托管实例”  以便填充托管实例的列表视图，在“实用工具资源管理器内容”  列表视图中右键单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称，然后选择“取消实例托管”  。  
  
##  <a name="create-a-new-utility-control-point-using-powershell"></a><a name="PowerShell_create_UCP"></a> 使用 PowerShell 创建新的实用工具控制点  
 使用以下示例创建一个新的实用工具控制点：  
  
```  
> $UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
> $SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
> $Utility = [Microsoft.SqlServer.Management.Utility.Utility]::CreateUtility("Utility", $SqlStoreConnection, "ProxyAccount", "ProxyAccountPassword");  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 实用工具的功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server 实用工具故障排除](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
