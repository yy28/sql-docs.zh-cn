---
title: "连接筛选器或文档 Web 部件的 SharePoint 集成模式下 |Microsoft 文档"
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
- Filter Web Part [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
- Documents Web Part [Reporting Services]
ms.assetid: 6a303135-c0ef-44cd-a423-1cea8df3dcf3
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5745964338889cd378a109636b2f6ebbdc32db26
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="connect-filter-or-documents-web-part---sharepoint-integrated-mode"></a>连接筛选器或文档 Web 部件的 SharePoint 集成模式下
  如果在使用 SharePoint 产品，可以创建一个包含筛选器 Web 部件或文档 Web 部件和报表查看器 Web 部件的面板或 Web 部件页。 支持的版本为 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]。 还支持 [!INCLUDE[winSPServ3](../../includes/winspserv3-md.md)] 或 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007。 通过连接筛选器 Web 部件，在筛选器 Web 部件中选择筛选器值的用户可以将值发送至同一页中的参数化报表。 通过连接文档 Web 部件，在文档库中单击报表的用户可以在相邻的报表查看器 Web 部件中查看报表。  
  
 筛选器 Web 部件可用于向报表中的一个或多个参数发送值。 若要使用筛选器 Web 部件，报表必须具有为其定义的参数并且参数与 Web 部件发送的值、数据类型及格式兼容。  
  
 文档 Web 部件与主文件夹站点的文档库相关联。 若要从文档库查看、添加或删除项，请单击 **“查看所有站点内容”**。 在“库”中，单击 **“文档”**。 可以使用 **“新建”**、 **“上载”**和 **“操作”** 菜单来管理文档库中的项。  
  
### <a name="to-connect-a-filter-web-part"></a>连接筛选器 Web 部件  
  
1.  打开或创建 Web 部件页或面板。  
  
2.  在 **“站点操作”** 菜单上，单击 **“编辑页面”**。  
  
3.  单击 **“添加 Web 部件”**。  
  
4.  在 **“所有 Web 部件”**的 **“杂项”** 类别中，选择 **“SQL Server Reporting Services 报表查看器”**。  
  
5.  单击 **“添加”**。 Web 部件将添加到区域的顶部。  
  
6.  在同一 Web 部件页或面板中的另一区域上，单击 **“添加 Web 部件”**。  
  
7.  在 **“所有 Web 部件”**的 **“筛选器”** 部分，选择一个 Web 部件。  
  
8.  单击 **“添加”**。 Web 部件将添加到区域的顶部。  
  
9. 在包含 Web 部件的区域中，单击 Web 部件的“编辑”菜单，依次指向“连接”、“发送筛选值到”，然后选择“报表查看器” - 报表名称。  
  
10. 签入更改并保存此页。  
  
### <a name="to-connect-a-documents-web-part"></a>连接文档 Web 部件  
  
1.  打开或创建 Web 部件页或面板。  
  
2.  在 **“站点操作”** 菜单上，单击 **“编辑页面”**。  
  
3.  单击 **“添加 Web 部件”**。  
  
4.  在 **“所有 Web 部件”**的 **“列表和库”** 部分中，选择 **“文档”**。  
  
5.  单击 **“添加”**。 Web 部件将添加到区域的顶部。  
  
6.  在工具窗格的底部，单击 **“应用”** ，然后单击 **“确定”** 关闭窗格。  
  
7.  在同一 Web 部件页或面板中的另一区域上，单击 **“添加 Web 部件”**。  
  
8.  在 **“所有 Web 部件”**的 **“杂项”** 类别中，选择 **“SQL Server Reporting Services 报表查看器”.**  
  
9. 单击 **“添加”**。 Web 部件将添加到区域的顶部。  
  
10. 在包含 Web 部件的区域中，单击 Web 部件的 **“编辑”** 菜单，依次指向 **“连接”**、 **“获取报表定义于”**，然后选择 **“文档”**。  
  
11. 签入更改并保存此页。  
  
## <a name="see-also"></a>另请参阅  
 [将报表查看器 Web 部件添加到网页（SharePoint 集成模式下的 Reporting Services）](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)   
 [在 SharePoint 站点上的报表查看器 Web 部件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [自定义报表查看器 Web 部件](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)  
  
  
