---
title: 比较不同 Microsoft 环境中的商业智能功能 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1fb759ee-8172-4c4c-9f7d-49af2c731006
caps.latest.revision: 18
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: ae54486aa141880189a012d897251604a292aefe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128508"
---
# <a name="compare-business-intelligence-capabilities-in-different-microsoft-environments"></a>比较不同 Microsoft 环境中的商业智能功能
  Microsoft[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]商业智能可部署在多个不同的环境包括[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 SharePoint Server、 SharePoint Online 和 Power BI for Office 365。 本主题将比较在各个环境中受支持的组件和功能。  
  
 有关比较 SharePoint Server 和 SharePoint Online 的详细信息，请参阅 [比较 SharePoint 计划和选项](http://products.office.com/SharePoint/compare-sharepoint-plans)。  
  
## <a name="author-and-manage-bi-reports-and-dashboards"></a>作者和管理 BI 报表和仪表板  
  
||SQL Server 2014 和 SharePoint Server 2013|SharePoint Online 计划 2|Power BI for Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|BI 网站|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 库|“否”|Power BI 网站|  
|数据管理以及查询共享和管理|“否”|“否”|是 **<sup>1</sup>**|  
|与 Master Data Services (MDS) 和 Data Quality Services (DQS) 的集成|是|否|“否”|  
|计划数据刷新|是，但不支持包含 Power Query 数据的工作薄|“否”|是|  
|自然语言查询 (Q&A)|“否”|“否”|是 **<sup>2</sup>**|  
|预测性的预测|“否”|“否”|是 **<sup>3</sup>**|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 集成|是|否|“否”|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 集成（多维式和表格式）|是|否|“否”|  
|将交互式 Power View 仪表板导出至 PowerPoint 演示文稿|是|否|“否”|  
|浏览器内的仪表板创作|是|否|“否”|  
|使用情况监视|是|否|是|  
|利用基于行的安全[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]多维数据集|是|否|“否”|  
  
 **<sup>1</sup>**[了解数据管理中的数据专员的角色](https://support.office.com/Article/Understanding-the-Role-of-Data-Stewards-in-Data-Management-ae3352f3-4389-45e8-a682-7fd6edb92524?ui=en-US&rs=en-US&ad=US)和[视频： Power BI 信息管理和数据管理](https://www.youtube.com/watch?v=8dHOj68ts7c)。    
  
 **<sup>2</sup>**[power BI q&a： 优化 Power BI 工作簿 （云建模）](https://support.office.com/article/Power-BI-Q-A-Optimize-a-Power-BI-workbook-cloud-modeling--96dc5941-d0f1-44e2-9d9d-c038a3a55849?ui=en-US&rs=en-US&ad=US)。    
  
 **<sup>3</sup>**[针对 Office 365 提供的新预测在 Power View 中的功能的简介](http://blogs.msdn.com/b/powerbi/archive/2014/05/08/introducing-new-forecasting-capabilities-in-power-view-for-office-365.aspx)。    
  
## <a name="view-and-browse-bi-data-reports-and-dashboards"></a>查看和浏览 BI 数据、报表和仪表板  
  
||SQL Server 2014 和 SharePoint Server 2013|SharePoint Online 计划 2|Power BI for Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|在浏览器中查看 Microsoft Excel 工作簿|是，前提是工作薄大小小于 2 GB|是，前提是工作簿大小小于 10 MB|是，前提是工作簿大小小于 250 GB|  
|HTML5 中的浏览器内数据浏览|“否”|否|是|  
|可远程访问报表和仪表板的移动 BI 应用|“否”|“否”|是 **<sup>1</sup>**|  
|Excel 工作簿包含[!INCLUDE[ssGemini](../includes/ssgemini-md.md)]作为数据源 **<sup>2</sup>**|是|否|“否”|  
|可以使用不同浏览器和版本中的功能|是，对于非 Power View 可视化效果 **<sup>3</sup>**|是，工作簿文件大小小于 10 MB  **<sup>3</sup>**|是 **<sup>3</sup>**|  
  
 **<sup>1</sup>**[Microsoft Power BI](http://apps.microsoft.com/windows/app/microsoft-power-bi/b7e7c94d-2ea3-4fa6-a277-9d19a1f697ba)。    
  
 **<sup>2</sup>**[作为数据源的 PowerPivot 工作簿  ](http://blogs.technet.com/b/excel_services__powerpivot_for_sharepoint_support_blog/archive/2013/02/15/powerpivot-workbook-as-a-data-source.aspx)  
  
 **<sup>3</sup>**[跨商业智能 (BI) 工具移动支持](http://msdn.microsoft.com/library/dn151146\(v=sql.110\).aspx)和[Planning for Reporting Services 和 Power View 浏览器支持 (Reporting Services 2014)](http://msdn.microsoft.com/library/ms156511.aspx)。    
  
## <a name="more-information"></a>详细信息  
  
-   [Excel、SharePoint Online 和 Power BI for Office 365 中的商业智能功能](https://technet.microsoft.com/en-us/library/dn198235.aspx)。  
  
-   有关使用同义词的要求的相关信息，请参阅 [向 Power Pivot Excel 数据模型添加同义词](https://support.office.com/Article/Add-synonyms-to-a-Power-Pivot-Excel-data-model-345f4f5b-5ec2-4998-bc46-a26bdc0810b6?ui=en-US&rs=en-US&ad=US)。  
  
-   [Office Online，选择你的企业社交网络：Yammer 还是 Newsfeed？](https://support.office.com/article/Pick-your-enterprise-social-network-Yammer-or-Newsfeed-21954c85-4384-47d4-96c2-dfa1c9d56e66?ui=en-US&rs=en-US&ad=US)。  
  
-   [Power BI for Office 365](http://www.microsoft.com/powerbi/default.aspx)。  
  
-   [Power BI 定价](http://www.microsoft.com/powerBI/pricing.aspx).  
  
-   [将 BI 中心网站与 Power BI for Office 365 网站相比较](http://technet.microsoft.com/library/dn394343\(v=office.15\).aspx)。  
  
-   [引入 Microsoft BI 报告和分析工具](http://go.microsoft.com/fwlink/p/?LinkId=617093)  
  
## <a name="community-content"></a>社区内容  
 [本地的 Microsoft 自服务 BI 对比云](http://businessintelligist.com/2014/02/07/microsoft-self-service-bi-on-premise-vs-could/).  
  
  