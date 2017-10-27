---
title: "将报表发布到 SharePoint 库 |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deploying [Reporting Services], reports in SharePoint integrated mode
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 3f6dfc28-50d8-4231-bd25-871b5f77cce6
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 88caf60aea658972b79c49948d882ce5f96e1d07
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="publish-a-report-to-a-sharepoint-library"></a>将报表发布到 SharePoint 库
  若要将报表发布到配置为 SharePoint 集成模式的 SharePoint 站点，必须在报表设计器中设置项目属性。 在项目属性中，对服务器、报表和共享数据源的所有引用都必须为完全限定的 URL。 在报表定义中，对子报表、钻取报表以及资源（如基于 Web 的图像）的所有引用都必须为完全限定的 URL。  
  
 必须对 SharePoint 站点拥有 **“成员”** 或 **“所有者”** 权限，才能设置项目的属性。 有关详细信息，请参阅 [SharePoint 模式下的报表服务器上已发布报表项的 URL 示例 (SSRS)](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)。  
  
### <a name="to-publish-a-report-to-a-sharepoint-site"></a>将报表发布到 SharePoint 站点  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开现有的或新的报表服务器项目。  
  
2.  在 **“项目”** 菜单中单击 **“属性”**。 *\<项目 >***属性页**对话框随即打开。  
  
3.  在 **“配置”** 列表中，选择要用于生成并发布报表的解决方案生成配置的名称。 当前配置被列为**Active**(*\<配置 >*)。  
  
4.  如果想在项目中发布共享数据源，并覆盖以前发布的共享数据源，请将 **OverwriteDataSources** 设置为 **True**。  
  
5.  （可选）对于 **TargetDataSourceFolder**，请键入指向 SharePoint 库或库文件夹的 URL（例如 `http://TestServer/TestSite/Documents/DataSources`）。  
  
     如果不指定值，将使用 **TargetReportFolder** 值。  
  
6.  对于 **TargetReportFolder**，请键入指向库或库文件夹的 URL（例如 `http://TestServer/TestSite/Documents/Reports`）。  
  
7.  对于 **TargetServerURL**，键入指向 SharePoint 顶级站点或子站点的 URL。 如果不指定站点，将使用默认顶级站点（例如 `http://servername`、 `http://servername/site`或 `http://servername/site/subsite`）。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. 在解决方案资源管理器中，右键单击要发布的报表，然后单击“部署”。 报表将发布到 **TargetReportFolder**中指定的位置。 部署错误将显示在输出窗口中。  
  
## <a name="see-also"></a>另请参阅  
 [“项目属性页”对话框](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [设置部署属性 (Reporting Services)](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
 [将报表发布到报表服务器](../../reporting-services/reports/publishing-reports-to-a-report-server.md)   
 [SharePoint 模式下的报表服务器上已发布报表项的 URL 示例 (SSRS)](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [使用 Office 数据连接 &#40;。odc &#41;使用报表 &#40;Reporting Services SharePoint 集成模式 &#41;](../../reporting-services/report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  

