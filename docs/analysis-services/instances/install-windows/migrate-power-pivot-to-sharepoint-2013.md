---
title: 将 Power Pivot 迁移到 SharePoint 2013 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 308b69e4da122bd409c4cbd12ec9196cb2da8317
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="migrate-power-pivot-to-sharepoint-2013"></a>将 Power Pivot 迁移到 SharePoint 2013
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  
  
 SharePoint 2013 不支持就地升级。 但是 **支持数据库附加升级**过程。 该行为不同于升级到 SharePoint 2010，在后者，客户可以在两个基本的升级方法（就地升级和数据库附加升级）之间进行选择。  
  
 如果您具有与 SharePoint 2010 相集成的 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 安装，则不能就地升级 SharePoint 服务器。 不过，您可以将内容数据库和服务应用程序数据库从 SharePoint 2010 场迁移到 SharePoint 2013 场。 本主题概要介绍了完成数据库附加升级以及完成与 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]以下内容相关的迁移所需的步骤：  
  
### <a name="migration-overview"></a>迁移概述  
  
|1|2|3|4|  
|-------|-------|-------|-------|  
|准备 SharePoint 2013 场|备份、复制、还原数据库。|装入内容数据库|迁移 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 计划|  
||[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|-SharePoint 管理中心<br /><br /> -Windows PowerShell|-SharePoint 应用程序页<br /><br /> -Windows PowerShell|  
  
##  <a name="bkmk_prepare_sharepoint2013"></a>准备 SharePoint 2013 场  
  
  > [!TIP]  
    >  查看为您的现有 Web 应用程序配置的身份验证方法。 SharePoint 2013 Web 应用程序默认为基于声明的身份验证。 为经典模式身份验证配置的 SharePoint 2010 Web 应用程序要求附加的步骤以便将数据库从 SharePoint 2010 迁移到 SharePoint 2013。 如果为经典模式身份验证配置了您的 Web 应用程序，则查看 SharePoint 2013 文档。  
  
1.  安装新的 SharePoint Server 2013 场。  
  
2.  在 SharePoint 模式中安装 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器的实例。 有关详细信息，请参阅 [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)。  
  
3.  在 SharePoint 场中的每台服务器上运行 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013 安装包 **spPowerPivot.msi** 。 有关详细信息，请参阅 [安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2013)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)。  
  
4.  在 SharePoint 2013 管理中心配置 Excel Services 服务应用程序，以使用在前面的步骤中创建的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] SharePoint 模式服务器。 有关详细信息，请参阅 [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)中的“配置基本 Analysis Services SharePoint 集成”一节。  
  
##  <a name="bkmk_backup_restore"></a>备份、 复制、 还原数据库  
 “SharePoint 数据库附加升级”过程是由多个步骤构成的一个序列，用于将 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 相关内容和服务应用程序数据库备份、复制和还原到 SharePoint 2013 场。  
  
1.  **将数据库设为只读：**在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中，右键单击数据库名称，然后单击“属性”。 在“选项”页中，将“数据库只读”属性设置为 **True**。  
  
2.  **备份：** 备份您要迁移到 SharePoint 2013 场的每个内容数据库和服务应用程序数据库。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中，右键单击数据库名称，再单击“任务”，然后单击“备份”。  
  
3.  将数据库备份文件 (.bak) 复制到所需的目标服务器。  
  
4.  **还原：** 将数据库还原到目标 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]。 可以使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 完成此步骤。  
  
5.  **将数据库设为读写：**将“数据库只读”设置为 **False**。  
  
##  <a name="bkmk_prepare_mount_databases"></a>准备 Web 应用程序和装入内容数据库  
 以下过程的更多详细说明，请参阅[将数据库从 SharePoint 2010 升级到 SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690) (http://go.microsoft.com/fwlink/p/?LinkId=256690)。  
  
1.  **使数据库脱机：**  
  
     使用 SharePoint 管理中心使每个 SharePoint 2013 内容数据库脱机。 内容数据库将被您所复制到的数据库替换。 考虑哪个顺序是针对您的环境的最佳顺序。 考虑首先使每个数据库脱机并装入其相关的替换数据库，然后再使下一内容数据库脱机。 另一个选项是使所有内容数据库作为一组而一起脱机。  
  
    1.  在 SharePoint 管理中心中，单击 **“应用程序管理”**。  
  
    2.  单击 **“管理内容数据库”**。  
  
    3.  单击数据库的名称。  
  
    4.  在 **“管理内容数据库设置”**上，将 **“数据库状态”** 设置为 **“脱机”**。  
  
    5.  选择 **“删除内容数据库”**。 请注意显示的警告：在内容数据库中存储的站点将无法继续访问。  
  
-   **装入内容数据库：**  
  
     使用 SharePoint 2013 Management shell 中的 PowerShell cmdlet 装入已迁移的内容数据库。 服务应用程序数据库不需要装载，只有的内容数据库： ![PowerShell 相关内容](../../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相关内容")  
  
    ```  
    Mount-SPContentDatabase "SharePoint_Content_O14-KJSP1" -DatabaseServer "[server name]\powerpivot" -WebApplication [web application URL]  
    ```  
  
     有关详细信息，请参阅[附加或分离内容数据库 (SharePoint Server 2010)](http://technet.microsoft.com/library/ff628582.aspx) (http://technet.microsoft.com/library/ff628582.aspx)。  
  
     **步骤完成时的状态：**  在装入操作完成时，用户可以看到已处于旧的内容数据库中的文件。 因此，用户可以在文档库中看到和打开工作簿。  
  
    -   > [!TIP]  
        >  在迁移过程中在此时可为迁移的工作簿创建新计划。 但是，这些计划在新的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序数据库中创建，而非您从旧的 SharePoint 场中复制的数据库。 因此，它们将不会包含任何旧计划。 在您完成以下步骤以便使用旧数据库和迁移旧计划后，新计划将不可用。  
  
### <a name="troubleshoot-issues-when-you-attempt-to-mount-databases"></a>解决在您尝试装入数据库时出现的问题  
 本节介绍在装入数据库时遇到的可能问题。  
  
1.  **身份验证错误：** 如果您看到与身份验证相关的错误，则查看源 Web 应用程序正在使用的身份验证模式。 该错误可能是由于身份验证在 SharePoint 2013 Web 应用程序和 SharePoint 2010 Web 应用程序之间不匹配导致的。 有关详细信息，请参阅 [1) 准备 SharePoint 2013 场](#bkmk_prepare_sharepoint2013) 。  
  
2.  **缺少 PowerPivot.Files：** 如果你看到与缺少 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .dlls 相关的错误，则 **spPowerPivot.msi** 尚未安装或者 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 配置工具尚未用于配置 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]。  
  
##  <a name="bkmk_upgrade_powerpivot_schedules"></a>升级 Power Pivot 计划  
 本节介绍了用于迁移 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 计划的详细信息和选项。 迁移计划是一个由两个步骤构成的过程。 首先将 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序配置为使用已迁移的服务应用程序数据库。 其次，选择用于计划迁移的两个选项之一。  
  
 **将服务应用程序配置为使用已迁移的服务应用程序数据库。**  
  
 在 SharePoint 管理中心中，将 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序配置为使用你复制到的旧服务应用程序数据库。 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务将服务应用程序数据库升级到新架构。  
  
1.  在 SharePoint 管理中心中，单击 **“管理服务应用程序”**。  
  
2.  查找 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序，例如“默认的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序”，在 SharePoint 功能区中单击服务应用程序的名称并单击  “属性”。  
  
3.  更新数据库服务器名称实例和数据库名称。 更新为您备份、复制和还原的数据库的正确名称。 在您单击 **“确定”**后，将升级服务应用程序数据库。 错误将位于 ULS 日志中。  
  
 **升级 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 计划**  
  
 配置 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序以便迁移刷新计划。  
  
-   **迁移计划选项 1：SharePoint 场管理员**  
  
    1.  在 SharePoint 2013 管理运行`Set-PowerPivotServiceApplication`cmdlet 与`-StartMigratingRefreshSchedules`开关以启用自动按需计划迁移![PowerShell 相关内容](../../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相关内容"). 下面的 Windows PowerShell 脚本假定只有一个 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序。  
  
        ```  
        $app=Get-PowerPivotServiceApplication  
        Set-PowerPivotServiceApplication $app -StartMigratingRefreshSchedules  
        ```  
  
         在运行 Windows PowerShell 脚本后，计划将处于活动状态并且计划将在下一个适当的时间运行。 但是，计划刷新页上的状态将不启用。 在计划首次运行时，将迁移该计划，并且在计划刷新页上，“已启用”   将为 true。  
  
    2.  如果您想要检查 StartMigratingRefreshSchedules 属性的当前值，则运行以下 PowerShell 脚本。 该脚本将遍历所有 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序对象并且显示名称和属性值：  
  
        ```  
        $apps = Get-PowerPivotServiceApplication  
        foreach ($app in $apps){}  
        Get-PowerPivotServiceApplication $appp | format-table -property displayname,id,StartMigratingRefreshSchedules  
        ```  
  
     **迁移计划选项 2：用户更新每个工作簿**  
  
    1.  另一个用于迁移计划的选项是对每个工作簿都启用计划刷新。 导航到包含工作簿的文档库。  
  
    2.  打开上下文菜单，然后单击**“管理[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]数据刷新”**。  
  
    3.  在 **“计划刷新”** 部分中，单击 **“启用”**。  
  
    4.  您可以选择 **“也尽快刷新”**。 此选项会在您单击“确定”后立即将一个刷新实例添加到队列中。 定期刷新计划仍将在适当的时间触发。  
  
    5.  单击 **“确定”**。 刷新历史记录现在将在刷新页中可见，并且刷新将在普通时间触发。  
  
 **SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿**  
  
-   在 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013 中使用时，SQL Server 2008 R2 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿将不会自动升级。 在您迁移包含 2008 R2 工作簿的内容数据库后，可以使用工作簿，但计划将不会升级。  
  
-   有关详细信息，请参阅 [升级工作簿和计划的数据刷新 (SharePoint 2013)](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)。  
  
##  <a name="bkmk_additional_resources"></a> 其他资源  
  
> [!NOTE]  
>  有关 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 和 SharePoint 数据库附加升级的详细信息，请参阅以下内容：  
  
-   [升级工作簿和计划的数据刷新 (SharePoint 2013)](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)。  
  
-   [到 SharePoint 2013 的升级过程概述](http://go.microsoft.com/fwlink/p/?LinkId=256688)(http://go.microsoft.com/fwlink/p/?LinkId=256688)。  
  
-   [清理升级到 SharePoint 2013 之前的准备工作](http://go.microsoft.com/fwlink/p/?LinkId=256689)(http://go.microsoft.com/fwlink/p/?LinkId=256689)。  
  
-   [将数据库从 SharePoint 2010 升级到 SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690) (http://go.microsoft.com/fwlink/p/?LinkId=256690)。  
  
  
