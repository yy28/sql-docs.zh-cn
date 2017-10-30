---
title: "将筛选器或文档 web 部件连接与 Reporting Services 报表查看器 web 部件 |Microsoft 文档"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 87d4b4a3f0c01804329f3a7b0688632c20ed6c9b
ms.contentlocale: zh-cn
ms.lasthandoff: 10/06/2017

---
# <a name="connect-filter-or-documents-web-part-with-a-reporting-services-report-viewer-web-part"></a>将筛选器或文档 web 部件连接与 Reporting Services 报表查看器 web 部件

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

如果你正在使用 SharePoint 产品，可以创建仪表板或 web 部件页，其中包含筛选器 web 部件或文档 web 部件和报表查看器 web 部件。 支持的版本为 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]。 还支持 [!INCLUDE[winSPServ3](../../includes/winspserv3-md.md)] 或 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007。 通过连接筛选器 web 部件，筛选器 web 部件中选择筛选器值的用户可以将值发送到同一页上的参数化报表。 通过连接文档 web 部件，用户单击文档库中的报表的可以在相邻的报表查看器 web 部件中查看报表。

> [!NOTE]
> 与 SharePoint 的 reporting Services 集成 SQL Server 2016 之后将不再可用。

 筛选器 web 部件用于将值发送到报表上的一个或多个参数。 若要使用筛选器 web 部件，该报表必须具有为其定义的参数与值、 数据类型和格式由 web 部件发送兼容。  
  
 文档 web 部件是与文档库的主文件夹站点关联。 若要从文档库查看、添加或删除项，请单击 **“查看所有站点内容”**。 在“库”中，单击 **“文档”**。 可以使用 **“新建”**、 **“上载”**和 **“操作”** 菜单来管理文档库中的项。  
  
## <a name="connect-a-filter-web-part"></a>连接筛选器 web 部件
  
1.  打开或创建 web 部件页或仪表板。  
  
2.  在 **“站点操作”** 菜单上，单击 **“编辑页面”**。  
  
3.  单击**添加 web 部件**。  
  
4.  在**所有 web 部件**中**杂项**类别中，选择**SQL Server Reporting Services 报表查看器**。  
  
5.  单击 **“添加”**。 Web 部件添加到该区域的顶部。  
  
6.  在相同的 web 部件页或仪表板中的另一个区域，单击**添加 web 部件**。  
  
7.  在**所有 web 部件**中**筛选器**部分中，选择 web 部件。  
  
8.  单击 **“添加”**。 Web 部件添加到该区域的顶部。  
  
9. 在包含 web 部件的区域，单击 web 部件**编辑**菜单上，指向**连接**，指向**发送筛选值到**，然后选择**报表查看器** - *报表名称*。  
  
10. 签入更改并保存此页。  
  
## <a name="connect-a-documents-web-part"></a>连接文档 web 部件  
  
1.  打开或创建 web 部件页或仪表板。  
  
2.  在 **“站点操作”** 菜单上，单击 **“编辑页面”**。  
  
3.  单击**添加 web 部件**。  
  
4.  在**所有 web 部件**中**列表和库**部分中，选择**文档。**  
  
5.  单击 **“添加”**。 Web 部件添加到该区域的顶部。  
  
6.  在工具窗格的底部，单击 **“应用”** ，然后单击 **“确定”** 关闭窗格。  
  
7.  在相同的 web 部件页或仪表板中的另一个区域，单击**添加 web 部件**。  
  
8.  在**所有 web 部件**中**杂项**类别中，选择**SQL Server Reporting Services 报表查看器。**  
  
9. 单击 **“添加”**。 Web 部件添加到该区域的顶部。  
  
10. 在包含 web 部件的区域，单击 web 部件**编辑**菜单上，指向**连接**，指向**获取报表定义于**，然后选择**文档**。  
  
11. 签入更改并保存此页。  
  
## <a name="see-also"></a>另请参阅

 [将报表查看器 web 部件添加到 web 页](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)   
 [在 SharePoint 站点上报表查看器 web 部件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [自定义报表查看器 Web 部件](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)  

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)

