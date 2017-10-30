---
title: "将报表查看器 web 部件添加到 web 页 |Microsoft 文档"
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
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 26080938c9849d6021f30d970ab2262f405df00c
ms.contentlocale: zh-cn
ms.lasthandoff: 10/06/2017

---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>将报表查看器 web 部件添加到 web 页

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

报表查看器 web 部件可用于查看报表，报表服务器配置上运行为在 SharePoint 集成模式。 Web 部件可用于显示报表生成器或报表设计器中创建并上载到库的报表定义 (.rdl) 文件。

如果你想要嵌入在该页上的报表，可以向网页中添加报表查看器 web 部件。

> [!NOTE]
> 本文是特定于报表查看器 web 部件随附了 Reporting Services 外接程序用于 SharePoint 产品。 与 SharePoint 的 reporting Services 集成 SQL Server 2016 之后将不再可用。

若要将 web 部件添加到网页上，必须在站点级别具有添加和自定义网页权限。 如果使用默认安全设置，此权限将授予拥有“完全控制”级权限的“所有者”  组的成员。

## <a name="to-embed-a-report-in-a-web-page"></a>若要将报表嵌入在网页中

1.  打开或创建 web 部件页或仪表板。  
  
2.  在 **“站点操作”**菜单上，单击 **“编辑页面”**。  
  
3.  单击**添加 web 部件**。  
  
4.  在 Web 部件类别列表中，选择 **“杂项”** 类别，然后选择 **“SQL Server Reporting Services 报表查看器”**。  
  
5.  单击 **“添加”**。 Web 部件添加到该区域的顶部。 可以将其拖至区域中的其他位置。  
  
6.  在查看器中，单击 **“单击此处打开工具窗格”**。  
  
7.  通过单击“浏览”(**...**) 按钮，从当前网站集合的任一库中选择报表。 也可以键入报表 URL。 若要确定任何报表的 URL，右键单击报表并选择**属性**。 请勿单击报表旁的向下箭头；报表项的“查看属性”页上未指出报表 URL。 如果你复制和粘贴的 URL**属性**对话框框中，将用空格的"%20"URL 编码 （例如，"公司 %20sales"应为"Company Sales"）。  
  
    > [!NOTE]  
    >  每个报表查看器 web 部件都包含一个报表。 URL 必须是当前 SharePoint 站点或同一 Web 应用程序或场内站点上的报表的完全限定路径。 URL 必须能解析为包含报表的文档库或文档库内的文件夹。 报表 URL 必须包含 .rdl 文件扩展名。 如果报表依赖的是模型或共享数据源文件，则不必在 URL 中指定这些文件。 报表包含对所需文件的引用。  
  
8.  在工具窗格打开时，可以通过设置属性来修改默认外观和布局。  
  
9. 在工具窗格的底部，单击 **“应用”** ，然后单击 **“确定”** 关闭窗格。  
  
## <a name="see-also"></a>另请参阅

 [在 SharePoint 站点上报表查看器 web 部件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [自定义报表查看器 web 部件](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [在 SharePoint 站点上授予对报表服务器项的权限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [安装或卸载用于 SharePoint 的 Reporting Services 外接程序](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  

