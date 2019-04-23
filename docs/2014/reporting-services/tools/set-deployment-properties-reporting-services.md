---
title: 设置部署属性 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], deploying
- publishing reports [Reporting Services]
- properties [Reporting Services], deployment
- deploying reports [Reporting Services]
ms.assetid: 18201ca0-bf4a-484f-b3a2-95d1046a6a9b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ab927ca95e32f1ad2a34a6e7910dd35a498eec0e
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59942873"
---
# <a name="set-deployment-properties-reporting-services"></a>设置部署属性 (Reporting Services)
  在[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，你必须指定报表服务器，并视需要指定报表文件夹和共享数据源，以便你可以将报表服务器项目中的项发布到报表服务器。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 生成、预览和部署报表所需的属性和值存储在报表服务器项目的项目配置中。 可以为这些项目属性创建多个命名集，从而方便地在属性集之间切换。 每个属性集都是一个配置。 例如，可拥有一个向测试服务器发布报表的配置，还可拥有另一个向生产服务器发布报表的配置。  
  
 使用配置管理器可以在项目配置中创建和管理项目属性集。 配置管理器是一项受 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]支持的功能， [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 正是基于此功能。  
  
> [!NOTE]  
>  请不要将此功能与 Reporting Services 配置管理器相混淆，后者用于在安装完成后配置 Reporting Services。 有关详细信息，请参阅[配置和管理报表服务器（SSRS 本机模式）](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，从报表服务器项目或解决方案发布报表的操作称为“部署报表”。  
  
### <a name="to-set-deployment-properties"></a>设置部署属性  
  
1.  右键单击报表项目，再单击“属性”。  
  
2.  在项目的 **“属性页”** 对话框中，从 **“配置”** 列表中选择要编辑的配置。 常用的配置有 **DebugLocal**、 **Debug**和 **Release**。  
  
    > [!NOTE]  
    >  您可以使用多种配置在不同的报表服务器或设置之间快速切换。  
  
3.  在中**OutputPath**文本框中，键入或粘贴本地文件系统来存储在生成验证、 部署和预览过程中使用的报表定义中的路径。 此路径必须与您用于项目的路径不同，并且它是一个相对路径（即项目路径下的一个子文件夹）。  
  
4.  在中**ErrorLevel**文本框中，键入问题生成的严重性报告为错误。 问题严重性生成报表、 数据源或其他项目资源时发生级别小于或等于的值**ErrorLevel**是报告为错误; 否则为将问题报告为警告。 任何错误都将导致生成任务失败。 有效的严重级别为 0 到 4（包括这两者）。 默认值为 2。  
  
     **ErrorLevel** 可用于增加或降低生成的敏感度。 例如，当在部署到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 报表服务器的过程中生成了一个带有地图的报表时，默认情况下将显示错误，并且报表生成过程失败。 如果您降低 **ErrorLevel** 并从报表中删除地图，则将显示警告并且报表生成过程继续。  
  
5.  在中**StartItem**列表中，选择要在预览窗口或浏览器窗口中显示报表项目运行时的报表。  
  
6.  在 **OverwriteDataSources** 列表中，选择 **True** 以在每次发布共享数据源时覆盖服务器上的共享数据源，或选择 **False** 以保留服务器上的数据源。  
  
7.  在中**TargetServerVersion**列表中，选择[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]版本[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]或选择**检测版本**以自动确定已安装的版本通过标识的服务器**TargetServer URL**属性。 默认值为 **SQL Server 2008 R2**。  
  
     使用 **TargetServerVersion** 可以自定义生成的报表，这些报表位于在 OutputPath 中指定的路径下，对应于在 **TargetServer URL**中指定的报表服务器版本。  
  
8.  在 **TargetDataSourceFolder** 文本框中，键入报表服务器上用于放置已发布共享数据源的文件夹。 **TargetDataSourceFolder** 的默认值为“数据源”。 如果保留此值为空白，则数据源将发布到 **TargetReportFolder**中指定的位置。  
  
9. 在 **TargetReportFolder** 文本框中，键入报表服务器上用于放置已发布报表的文件夹。 默认值为**TargetReportFolder**是报表项目的名称。  
  
    > [!NOTE]  
    >  对于在本机模式下运行的报表服务器，必须拥有对目标文件夹的 **“发布”** 权限，才能将报表发布到该文件夹。 发布权限通过角色分配提供，此角色分配将用户帐户映射到包括发布操作的角色。 有关详细信息，请参阅 [创建和管理角色分配](../security/create-and-manage-role-assignments.md)。 对于在 SharePoint 集成模式下运行的报表服务器，必须拥有对 SharePoint 站点的 **“成员”** 或 **“所有者”** 权限。 有关详细信息，请参阅 [报表服务器项的 SharePoint 站点和列表权限参考](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)。  
  
10. 在 **TargetServerURL** 文本框中，键入目标报表服务器的 URL。 在发布报表之前，必须将此属性设置为有效的报表服务器 URL。 向在本机模式下运行的报表服务器发布时，请使用报表服务器虚拟目录的 URL（例如，http:*//server/reportserver* 或 https:*//server/reportserver*）。 这是报表服务器的虚拟目录，而不是报表管理器的虚拟目录。  
  
     发布到在 SharePoint 集成模式下运行的报表服务器时，请使用 SharePoint 顶级站点或子站点的 URL。 如果不指定站点，将使用默认顶级站点（例如 http://*servername*、 http://*servername*/*site* 或 http://*servername*/*site*/*subsite*）。  
  
### <a name="to-set-configuration-manager-properties"></a>设置配置管理器属性  
  
1.  右键单击报表项目，再单击“属性”。  
  
2.  在该项目的 **“属性页”** 对话框中，单击 **“配置管理器”**。  
  
3.  在 **“配置管理器”** 对话框中，选择要编辑的配置。 当前有效的配置显示为“活动(***\<配置>***)”。  
  
4.  在 **“项目上下文”** 中，为解决方案中的每个项目选中或清除 **“生成”** 或 **“部署”**。  
  
    > [!NOTE]  
    >  如果选中 **“生成”** ，报表设计器将生成报表项目，并在预览或发布到报表服务器之前检查错误。 如果选中 **“部署”** ，报表设计器将按照部署属性中的定义，将报表发布到报表服务器。 如果未选中 **“部署”** ，报表设计器将在本地预览窗口中显示在 **StartItem** 属性中指定的报表。  
  
## <a name="see-also"></a>请参阅  
 [发布数据源和报表](../reports/publishing-data-sources-and-reports.md)   
 [预览报表](../reports/previewing-reports.md)   
 [报表设计器的 F1 帮助](report-designer-f1-help.md)   
 [SharePoint 模式下的报表服务器上已发布报表项的 URL 示例 (SSRS)](url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [“项目属性页”对话框](project-property-pages-dialog-box.md)   
 [将报表发布到报表服务器](../reports/publishing-reports-to-a-report-server.md)  
  
  
