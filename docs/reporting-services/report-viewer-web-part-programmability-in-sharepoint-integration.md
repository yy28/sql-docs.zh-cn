---
title: "报表查看器 Web 部件在 SharePoint 集成的可编程性 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 714017b7-1bd6-4950-a3c6-d0df8450a877
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 9339b0f383efd757e9be49271f4a5bdd2d7a4d4f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="report-viewer-web-part-programmability-in-sharepoint-integration"></a>SharePoint 集成中的报表查看器 Web 部件可编程性
  报表查看器 Web 部件是一个包含一组公共应用程序编程接口 (API)，使开发人员可以创建自定义 SharePoint 应用程序的服务器控件。 您可以创建自定义 Web 部件，以使用 Web 部件连接向报表查看器 Web 部件提供报表路径和参数。 还可以在自定义 SharePoint Web 部件页中嵌入 Web 部件，并使用该公共 API 对其进行自定义。  
  
## <a name="connecting-to-report-viewer-web-part-with-custom-web-parts"></a>使用自定义 Web 部件连接到报表查看器 Web 部件  
 报表查看器 Web 部件是连接使用者实现的 SharePoint Web 部件到<xref:System.Web.UI.WebControls.WebParts.IWebPartRow>或 T:Microsoft.SharePoint.WebPartPages.IFilterValues。 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web 部件，如**文档**Web 部件可以提供报表查看器 Web 部件时将作为报表查看器 Web 部件相同的 Web 部件页面上放置的报表路径。 同样，T:Microsoft.SharePoint.WebPartPages.IFilterValues Web 部件，如**文本筛选器**或**选择筛选器**，可以提供报表查看器 Web 部件时将作为报表查看器 Web 部件相同的 Web 部件页面上放置的报表参数。  
  
### <a name="implementing-a-report-path-provider-with-iwebpartrow"></a>使用 IWebPartRow 实现报表路径访问接口  
 若要通过 Web 部件连接向报表查看器 Web 部件提供报表路径，请执行以下操作：  
  
1.  创建一个实现 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 接口的 Web 部件。  
  
2.  将 Web 部件添加到与报表查看器 Web 部件所在的相同 Web 部件页。  
  
3.  在基于 Web 的 Web 部件设计用户界面中将 Web 部件连接到报表查看器 Web 部件。  
  
    > [!NOTE]  
    >  你只能连接一个<xref:System.Web.UI.WebControls.WebParts.IWebPartRow>Web 部件连接到报表查看器 Web 部件时，你无法连接同时<xref:System.Web.UI.WebControls.WebParts.IWebPartRow>到报表查看器 Web 部件，同时 T:Microsoft.SharePoint.WebPartPages.IFilterValues Web 部件和 Web 部件。  
  
 为你<xref:System.Web.UI.WebControls.WebParts.IWebPartRow>Web 部件，要正确使用 T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart，你必须执行以下操作<xref:System.Web.UI.WebControls.WebParts.IWebPartRow.GetRowData%2A>方法：  
  
-   使用 <xref:System.Data.DataRowView> 对象作为输入参数调用回调方法。  
  
-   确保 <xref:System.Data.DataRowView> 对象包含一个名为“DocUrl”的列，该列包含报表路径。  
  
    > [!NOTE]  
    >  [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2010 的外接程序中的报表查看器 Web 部件还支持使用“FileRef”列来接收报表路径。  
  
### <a name="implementing-a-report-parameter-provider-with-ifiltervalues"></a>使用 IfilterValues 实现报表参数访问接口  
 Web 部件实现 T:Microsoft.SharePoint.WebPartPages.IFilterValues 可以向报表查看器 Web 部件提供一个参数值。 发送到报表查看器 Web 部件的参数值可能会受到与在报表定义中指定的报表参数相同的限制，如数据类型、有效值等。  
  
 若要向报表查看器 Web 部件提供报表参数，请执行以下操作：  
  
1.  创建 Web 部件实现 T:Microsoft.SharePoint.WebPartPages.IFilterValues 接口。  
  
2.  将 Web 部件添加到与 T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart 相同的页。  
  
3.  连接到基于 Web 的 Web 部件设计用户界面中的报表查看器 Web 部件 T:Microsoft.SharePoint.WebPartPages.IFilterValues Web 部件。  
  
    > [!NOTE]  
    >  你可以一次连接到报表查看器 Web 部件的多个 T:Microsoft.SharePoint.WebPartPages.IFilterValues Web 部件。 但是，无法连接同时<xref:System.Web.UI.WebControls.WebParts.IWebPartRow>到报表查看器 Web 部件，同时 T:Microsoft.SharePoint.WebPartPages.IFilterValues Web 部件和 Web 部件。  
  
  
