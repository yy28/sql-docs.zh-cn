---
title: 更改 SQL Server 的服务启动帐户（SQL Server 配置管理器） |Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server services, startup account changes
- startup accounts [SQL Server]
- changing startup accounts for services
ms.assetid: d721c796-0397-46a7-901b-1a9a3c3fb385
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 105592676413fb43c4cac5b572623096a517b147
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935089"
---
# <a name="change-the-service-startup-account-for-sql-server-sql-server-configuration-manager"></a>为 SQL Server 更改服务启动帐户（SQL Server 配置管理器）
  本主题介绍如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的启动选项，以及更改由 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 使用的服务帐户。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]或 PowerShell。 有关如何选择适合的服务帐户的详细信息，请参阅 [配置 Windows 服务帐户和权限](configure-windows-service-accounts-and-permissions.md)。  
  
> [!IMPORTANT]  
>  更改 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的服务启动帐户后，必须重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务（ [!INCLUDE[ssDE](../../includes/ssde-md.md)]）才能使更改生效。 重新启动此服务时，所有与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例关联的数据库在此服务成功重新启动后才能使用。 如果必须更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的服务启动帐户，请确保在定期计划维护期间或者数据库可以脱机（不中断日常操作）时执行此操作。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   群集服务器  
  
     必须从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 群集的活动节点更改由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 使用的服务帐户。  
  
     如果运行在 Windows Server 2008 上（在一个使用域组的非默认配置中），则更改由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理使用的服务帐户时，需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器，通过使资源组脱机来停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   SKU 升级（从[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 到 Express 以外的 SKU）  
  
     在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 安装期间， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务被配置为使用 Network Service 帐户（但已禁用）。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器可以更改为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务分配的帐户，但不能启用或启动该服务。 将 SKU 从 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 升级到 Express 以外的版本后，不能自动启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务，但可以在需要时通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器以及将服务启动模式更改为“手动”或“自动”来启用该服务。  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> 使用 SQL Server 配置管理器  
  
#### <a name="to-change-the-sql-server-service-startup-account"></a>更改 SQL Server 服务启动帐户  
  
1.  在 **“开始”** 菜单中，依次指向 **“所有程序”** 、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、 **“配置工具”** ，然后单击 **“SQL Server 配置管理器”** 。  
  
    > [!NOTE]  
    >  因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台程序的一个管理单元而不是单独的程序，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器在新版本的 Windows 中不显示为一个应用程序。  
    >   
    >  -   **Windows 10**：  
    >          若要打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager，请在 "**开始" 页**上键入 sqlservermanager12.msc （对于 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ）。 对于早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请将 12 替换为较小的数字。 单击 SQLServerManager12.msc 可打开“配置管理器”。 若要将 Configuration Manager 固定到 "起始页" 或 "任务栏"，请右键单击 "Sqlservermanager12.msc"，然后单击 "**打开文件位置**"。 在 Windows 文件资源管理器中，右键单击 "Sqlservermanager12.msc"，然后单击 "**固定到****任务栏**"。  
    > -   **Windows 8**：  
    >          若要打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager，请在 "**搜索**" 超级按钮中的 "**应用**" 下，键入**sqlservermanager version>.msc （ \<version> **如 `SQLServerManager12.msc` ），然后按**enter**。  
  
2.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器中，单击 **“SQL Server 服务”** 。  
  
3.  在详细信息窗格中，右键单击要为其更改服务启动帐户的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称，再单击“属性”  。  
  
4.  在 " **SQL Server \<***instancename***> 属性**" 对话框中，单击 "**登录**" 选项卡，然后选择 "**登录身份**" 帐户类型。  
  
5.  选择了新服务启动帐户后，单击 **“确定”** 。  
  
     将出现一个消息框，询问是否要重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。  
  
6.  单击 **“是”** ，然后关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。  
  
## <a name="see-also"></a>另请参阅  
 [启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务](start-stop-pause-resume-restart-sql-server-services.md)   
 [在 SQL Server 工具中将 WMI 配置为显示服务器状态](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
