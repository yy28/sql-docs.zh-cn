---
title: 什么&#39;中 Analysis Services 和 Business Intelligence |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: aa69c299-b8f4-4969-86d8-b3292fe13f08
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a6b59ae2bd1c9d21704d87289b604feefa326f1e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054337"
---
# <a name="what39s-new-in-analysis-services-and-business-intelligence"></a>什么&#39;中 Analysis Services 和 Business Intelligence
  添加了支持针对多维模型的 Power View 报表的功能除外[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]以前的版本相比未发生更改。  
  
 有关其他信息[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]产品和技术的此版本中，请参阅[What's New in SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md)。  
  
## <a name="updates-to-design-tool-installation"></a>设计工具安装更新  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] for Business Intelligence (SSDT-BI)（以前称为 Business Intelligence Development Studio (BIDS)）用于创建 Analysis Services 模型、Reporting Services 报表和 Integration Services 包。 您可以从以下位置下载 SSDT-BI：  
  
-   [下载 SSDT-BI for Visual Studio 2013](http://go.microsoft.com/fwlink/p/?LinkId=396526)  
  
-   [下载 SSDT-BI for Visual Studio 2012](http://go.microsoft.com/fwlink/p/?LinkID=273673)  
  
 如果计算机上装有旧版 SSDT-BI 或 BIDS，则新版与旧版并行安装。 在一个工作站上同时运行新版和旧版的设计工具是很常见的，这样可以修改与特定服务器版本关联的项目和解决方案。  
  
> [!NOTE]  
>  有多个下载站点可下载 SSDT 的 Visual Studio 2012 和 Visual Studio 2013 版本。 大多不含 BI 项目模板。 使用上面的链接可获得正确的版本。 如果看到 Business Intelligence 项目模板文件夹，即说明 SSDT-BI 的版本正确无误。 此文件夹包含 Analysis Services、Reporting Services 和 Integration Services 的项目模板。 根据安装 SSDT-BI 的方式，可能还会看到一个 SQL Server 数据库项目模板。  
  
 ![SSDT 中新的项目模板](media/ssdt-biprojects.png "New Project templates in SSDT")  
  
## <a name="features-recently-added-power-view-for-multidimensional-models"></a>最近添加的功能：用于多维模型的 Power View  
 针对多维模型创建 Power View 报表的功能最先是在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 1 累积更新 4 中引入的。 用于多维模型的 Power View 现在包含在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中。  
  
 **多维模型的 power View 报表**  
  
 ![Power View 报表](media/powerviewreport-wn.gif "Power View 报表")  
  
 此功能通过使多维模型（也称为 OLAP 多维数据集）可以与最新客户端报告工具一起使用，帮助组织最大程度利用现有的 BI 投资。 根据多维模型中的数据类型，用户可以方便地创建各种动态可视化对象，从表和矩阵到气泡图和地理图。 多维模型现在还支持使用数据分析表达式 (DAX) 进行查询。  
  
 多维模型的 power View 要求中的内置 Power View 报告功能[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] （在 SharePoint 模式下）。 其他版本的 Power View（特别是 Excel 2013 中的 Power View 外接程序）不支持多维模型。  
  
 若要了解详细信息，请参阅[多维模型的 Power View](http://msdn.microsoft.com/library/dn140246.aspx)。  
  
  
