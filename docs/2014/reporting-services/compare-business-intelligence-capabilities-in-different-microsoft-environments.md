---
title: 比较不同 Microsoft 环境中的商业智能功能 |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 12/15/2019
ms.openlocfilehash: 3305e682f6ccbbee4ac9710e29ae522eb7339910
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241211"
---
# <a name="compare-business-intelligence-capabilities-in-different-microsoft-environments"></a>比较不同 Microsoft 环境中的商业智能功能

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 商业智能可部署在多个不同环境中，包括带有 SharePoint Server、SharePoint Online 和 Power BI for Office 365 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 本主题将比较在各个环境中受支持的组件和功能。  
  
有关比较 SharePoint Server 和 SharePoint Online 的详细信息，请参阅 [比较 SharePoint 计划和选项](https://products.office.com/SharePoint/compare-sharepoint-plans)。  
  
## <a name="author-and-manage-bi-reports-and-dashboards"></a>作者和管理 BI 报表和仪表板  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online 计划 2|Power BI for Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|BI 网站|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)]图库|否|Power BI 网站|  
|数据管理以及查询共享和管理|否|否|是** <sup>1</sup>**|  
|与 Master Data Services (MDS) 和 Data Quality Services (DQS) 的集成|是|否|否|  
|计划数据刷新|是，但不支持包含 Power Query 数据的工作薄|否|是|  
|自然语言查询（Q&）|否|否|是** <sup>2</sup>**|  
|预测性的预测|否|否|是** <sup>3</sup>**|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]集成度|是|否|否|  
|
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 集成（多维式和表格式）|是|否|否|  
|将交互式 Power View 仪表板导出至 PowerPoint 演示文稿|是|否|否|  
|浏览器内的仪表板创作|是|否|否|  
|使用情况监视|是|否|是|  
|利用基于行的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多维数据集的安全性|是|否|否|  
|||||

 **<sup>1</sup>**  [了解数据管理和视频中数据专员](https://support.office.com/Article/Understanding-the-Role-of-Data-Stewards-in-Data-Management-ae3352f3-4389-45e8-a682-7fd6edb92524?ui=en-US&rs=en-US&ad=US)的角色[： Power BI 信息管理和数据管理](https://www.youtube.com/watch?v=8dHOj68ts7c)。  
  
 **<sup>2</sup>**  [Power BI Q&：优化 Power BI 工作簿（云建模）](https://powerbi.microsoft.com/nl-nl/blog/new-in-power-bi-cloud-modeling-for-q-and-a/)。  
  
 **<sup>3</sup>**  [为 Office 365 在 Power View 中引入了新的预测功能](https://blogs.msdn.com/b/powerbi/archive/2014/05/08/introducing-new-forecasting-capabilities-in-power-view-for-office-365.aspx)。  
  
## <a name="view-and-browse-bi-data-reports-and-dashboards"></a>查看和浏览 BI 数据、报表和仪表板  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online 计划 2|Power BI for Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|在浏览器中查看 Microsoft Excel 工作簿|是，前提是工作薄大小小于 2 GB|是，前提是工作簿大小小于 10 MB|是，前提是工作簿大小小于 250 GB|  
|HTML5 中的浏览器内数据浏览|否|否|是|  
|可远程访问报表和仪表板的移动 BI 应用|否|否|是** <sup>1</sup>**|  
|Excel 工作薄，其中 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 作为数据源 **<sup>2</sup>**|是|否|否|  
|可以使用不同浏览器和版本中的功能|是，针对非 Power View 可视化效果 **<sup>3</sup>**|是，因为工作薄文件大小小于 10 MB **<sup>3</sup>**|是** <sup>3</sup>**|  
|||||

 **<sup>1</sup>**  [Microsoft Power BI](https://apps.microsoft.com/windows/app/microsoft-power-bi/b7e7c94d-2ea3-4fa6-a277-9d19a1f697ba)。  
  
 **<sup>2</sup>**  [作为数据源的 PowerPivot 工作簿](https://blogs.technet.com/b/excel_services__powerpivot_for_sharepoint_support_blog/archive/2013/02/15/powerpivot-workbook-as-a-data-source.aspx)  
  
 **<sup>3</sup>**  [跨商业智能（BI）工具的移动支持](https://msdn.microsoft.com/library/dn151146\(v=sql.110\).aspx)以及[规划 Reporting Services 和 Power View 浏览器支持（Reporting Services 2014）](https://msdn.microsoft.com/library/ms156511.aspx)。  
  
## <a name="more-information"></a>详细信息  
  
- [Excel 和 Office 365 中的 BI 功能](https://support.office.com/article/BI-capabilities-in-Excel-and-Office-365-26c0548e-124c-4fd3-aab3-5f64568cb743)。  
  
- 有关使用同义词的要求的信息，请参阅在 pragmaticworks.com 中[优化 Power BI Q&A With 同义词 & 句式](https://blog.pragmaticworks.com/optimizing-power-bi-qa-with-synonyms-phrasing-using-cloud-modeling)。  
  
- [Office Online，请选择你的企业社交网络： Yammer 或新闻源？](https://support.office.com/article/Pick-your-enterprise-social-network-Yammer-or-Newsfeed-21954c85-4384-47d4-96c2-dfa1c9d56e66?ui=en-US&rs=en-US&ad=US)。  
  
- [Power BI for Office 365](https://www.microsoft.com/powerbi/default.aspx)。  
  
- [定价 Power BI](https://www.microsoft.com/powerBI/pricing.aspx)。  
  
- [使用 Microsoft 商业智能 (BI) 工具进行分析和报告](../reporting-services/choosing-microsoft-business-intelligence-bi-tools-for-analysis-and-reporting.md)  
  
## <a name="community-content"></a>社区内容

