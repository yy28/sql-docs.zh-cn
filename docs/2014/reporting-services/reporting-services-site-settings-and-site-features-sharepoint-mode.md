---
title: Reporting Services 网站设置和网站功能 （SharePoint 模式） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e0040fec-e2b7-4099-ae01-3b9bb9128bbd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 14708d286ea11a872a3260f41cae44e05e7fb30c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63283404"
---
# <a name="reporting-services-site-settings-and-site-featuressharepoint-mode"></a>Reporting Services 网站设置和网站功能（SharePoint 模式）
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式具有几个网站级自定义功能和可以从“SharePoint 网站设置”页管理的网站功能。 这些设置适用于整个网站并影响所有 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序。 必须拥有“内容管理员”和“系统管理员”权限才能查看此页。  
  
|网站设置|Description|  
|------------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 网站设置|本主题中介绍了适用于网站的设置。|  
|管理数据警报|管理数据警报功能。|  
|报表服务器文件同步|默认情况下停用的网站级功能。<br /><br /> 在文档库中直接添加或更新文件时，将报表服务器文件（.rdl、.rsds、.smdl、.rsd、.rsc、.rdlx）从 SharePoint 文档库同步到报表服务器。<br /><br /> 有关详细信息，请参阅 [在 SharePoint 管理中心中激活报表服务器文件同步功能](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)|  
  
## <a name="to-open-the-reporting-services-site-settings-page"></a>打开 Reporting Services“网站设置”页  
  
1.  从 SharePoint 站点**站点操作**菜单上，单击**站点设置**。  
  
2.  在 **Reporting Services** 部分中，单击 **“Reporting Services 网站设置”**。  
  
## <a name="options-for-reporting-services-site-settings"></a>Reporting Services 网站设置选项  
  
|Option|Description|  
|------------|-----------------|  
|**启用 RSClientPrint ActiveX 控件下载**|该控件显示一个自定义打印对话框，它支持其他打印对话框常见的功能，包括打印预览、指定特定页和范围的页面选择、页边距和打印方向等功能。 有关控件的详细信息，请参阅 [Using the RSClientPrint Control in Custom Applications](report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**启用本地模式下的远程错误**|在本地模式下运行时，在远程计算机上显示或隐藏详细的错误消息。 如果看到类似于以下内容的错误消息，则启用远程错误可能很有用：<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**启用报表的辅助功能元数据**|启用报表的 HTML 输出中的辅助功能元数据|  
|**启用报表的精确数据可视化调整大小**|配置 tablix 中数据可视化调整大小行为以完全适合。 这包括图表、仪表和地图。 禁用该行为（即数据可视化对象为大致适合时），可能留下一些空格。 此设置仅适用于在报表查看器 Web 部件中呈现。 若要为服务器端呈现管理此行为，需要修改 **rsreportserver.config** 文件。 有关详细信息，请参见以下内容：<br /><br /> [RSReportServer 配置文件](report-server/rsreportserver-config-configuration-file.md)。<br /><br /> [Customize Rendering Extension Parameters in RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)。<br /><br /> [HTML Device Information Settings](html-device-information-settings.md)。<br /><br /> 启用“精确”可能会影响性能，因为确定精确大小所需的处理时间可能比大致适合时所需的时间长。|  
  
## <a name="see-also"></a>请参阅  
 [管理 Reporting Services SharePoint 服务应用程序](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
