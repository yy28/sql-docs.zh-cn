---
title: 将报表发布到 SharePoint 库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], reports in SharePoint integrated mode
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 3f6dfc28-50d8-4231-bd25-871b5f77cce6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 24888d53a8e18ba861df2aa0df0261c64445494f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59936813"
---
# <a name="publish-a-report-to-a-sharepoint-library"></a>将报表发布到 SharePoint 库
  若要将报表发布到配置为 SharePoint 集成模式的 SharePoint 站点，必须在报表设计器中设置项目属性。 在项目属性中，对服务器、报表和共享数据源的所有引用都必须为完全限定的 URL。 在报表定义中，对子报表、钻取报表以及资源（如基于 Web 的图像）的所有引用都必须为完全限定的 URL。  
  
 必须对 SharePoint 站点拥有 **“成员”** 或 **“所有者”** 权限，才能设置项目的属性。 有关详细信息，请参阅 [SharePoint 模式下的报表服务器上已发布报表项的 URL 示例 (SSRS)](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)。  
  
### <a name="to-publish-a-report-to-a-sharepoint-site"></a>将报表发布到 SharePoint 站点  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开现有的或新的报表服务器项目。  
  
2.  在 **“项目”** 菜单中单击 **“属性”**。 “\<项目>属性页”对话框即会打开。  
  
3.  在 **“配置”** 列表中，选择要用于生成并发布报表的解决方案生成配置的名称。 当前配置以“活动”状态列出（\<配置>）。  
  
4.  如果想在项目中发布共享数据源，并覆盖以前发布的共享数据源，请将 **OverwriteDataSources** 设置为 **True**。  
  
5.  （可选）有关**TargetDataSourceFolder**，键入指向 SharePoint 库或库文件夹的 URL (例如， *http://TestServer/TestSite/Documents/DataSources)*。  
  
     如果不指定值，将使用 **TargetReportFolder** 值。  
  
6.  有关**TargetReportFolder**，键入指向库或库文件夹的 URL (例如， *http://TestServer/TestSite/Documents/Reports)*。  
  
7.  对于 **TargetServerURL**，键入指向 SharePoint 顶级站点或子站点的 URL。 如果不指定站点，则使用默认顶级站点 (例如， *http://servername*， *http://servername/site*，或者*http://servername/site/subsite*)。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. 在解决方案资源管理器中，右键单击要发布的报表，然后单击“部署”。 报表将发布到 **TargetReportFolder**中指定的位置。 部署错误将显示在输出窗口中。  
  
## <a name="see-also"></a>请参阅  
 [“项目属性页”对话框](../tools/project-property-pages-dialog-box.md)   
 [设置部署属性 (Reporting Services)](../tools/set-deployment-properties-reporting-services.md)   
 [将报表发布到报表服务器](publishing-reports-to-a-report-server.md)   
 [SharePoint 模式下的报表服务器上已发布报表项的 URL 示例 (SSRS)](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [将 Office 数据连接 (.odc) 用于报表（SharePoint 集成模式下的 Reporting Services）](../report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  
