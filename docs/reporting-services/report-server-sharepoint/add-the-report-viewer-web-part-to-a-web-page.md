---
title: 将报表查看器 Web 部件添加到网页 | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5d9eb107d1355a15d15c22fc3b24824cae009075
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>将报表查看器 Web 部件添加到网页

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

可以使用报表查看器 Web 部件查看在报表服务器（配置为在 SharePoint 集成模式下运行）上运行的报表。 可以使用 Web 部件显示你在报表生成器或报表设计器中创建并上传到库中的报表定义 (.rdl) 文件。

如果要在网页中嵌入报表，则可以向该网页添加报表查看器 Web 部件。

> [!NOTE]
> 本文专门针对用于 SharePoint 产品的 Reporting Services 外接程序附带的 Report Viewer Web 部件。 自 SQL Server 2016 之后，不再提供 Reporting Services 与 SharePoint 的集成这一功能。

若要向网页中添加 Web 部件，则必须拥有站点级别的“添加和自定义页面”权限。 如果使用默认安全设置，此权限将授予拥有“完全控制”级权限的“所有者”  组的成员。

## <a name="to-embed-a-report-in-a-web-page"></a>将报表嵌入网页中

1.  打开或创建 Web 部件页或仪表板。  
  
2.  在 **“站点操作”**菜单上，单击 **“编辑页面”**。  
  
3.  单击“添加 Web 部件”。  
  
4.  在 Web 部件类别列表中，选择 **“杂项”** 类别，然后选择 **“SQL Server Reporting Services 报表查看器”**。  
  
5.  单击 **“添加”**。 Web 部件将添加到区域的顶部。 可以将其拖至区域中的其他位置。  
  
6.  在查看器中，单击 **“单击此处打开工具窗格”**。  
  
7.  通过单击“浏览”(**...**) 按钮，从当前网站集合的任一库中选择报表。 也可以键入报表 URL。 若要确定任一报表的 URL，请右键单击报表并选择“属性”。 请勿单击报表旁的向下箭头；报表项的“查看属性”页上未指出报表 URL。 如果从“属性”对话框复制并粘贴 URL，请用空格替换“%20”URL 编码（例如，“Company%20Sales”应为“Company Sales”）。  
  
    > [!NOTE]  
    >  每个报表查看器 Web 部件都包含一个报表。 URL 必须是当前 SharePoint 站点或同一 Web 应用程序或场内站点上的报表的完全限定路径。 URL 必须能解析为包含报表的文档库或文档库内的文件夹。 报表 URL 必须包含 .rdl 文件扩展名。 如果报表依赖的是模型或共享数据源文件，则不必在 URL 中指定这些文件。 报表包含对所需文件的引用。  
  
8.  在工具窗格打开时，可以通过设置属性来修改默认外观和布局。  
  
9. 在工具窗格的底部，单击 **“应用”** ，然后单击 **“确定”** 关闭窗格。  
  
## <a name="see-also"></a>另请参阅

 [SharePoint 站点上的报表查看器 Web 部件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [自定义报表查看器 Web 部件](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [在 SharePoint 站点上授予对报表服务器项的权限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [安装或卸载用于 SharePoint 的 Reporting Services 外接程序](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
