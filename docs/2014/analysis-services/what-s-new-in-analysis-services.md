---
title: Analysis Services 和商业智能中&#39;的新增功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/07/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: aa69c299-b8f4-4969-86d8-b3292fe13f08
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1458dcf473ffbf7fc9bab13c2c688a4e01954c56
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175536"
---
# <a name="what39s-new-in-sql-server-2014-analysis-services"></a>SQL Server 2014 中的新增功能&#39;Analysis Services
  除了添加支持多维模型的 Power View 报表的功能之外， [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]与以前的版本相比，没有任何变化。

 有关此版本中[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]其他产品和技术的详细信息，请参阅[SQL Server 2014 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)。

## <a name="updates-to-design-tool-installation"></a>设计工具安装更新
 
  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] for Business Intelligence (SSDT-BI)（以前称为 Business Intelligence Development Studio (BIDS)）用于创建 Analysis Services 模型、Reporting Services 报表和 Integration Services 包。 您可以从以下位置下载 SSDT-BI：

-   [下载 SSDT-BI for Visual Studio 2013](https://go.microsoft.com/fwlink/p/?LinkId=396526)

-   [下载 SSDT-BI for Visual Studio 2012](https://go.microsoft.com/fwlink/p/?LinkID=273673)

 如果计算机上装有旧版 SSDT-BI 或 BIDS，则新版与旧版并行安装。 在一个工作站上同时运行新版和旧版的设计工具是很常见的，这样可以修改与特定服务器版本关联的项目和解决方案。

> [!NOTE]
>  有多个下载站点可下载 SSDT 的 Visual Studio 2012 和 Visual Studio 2013 版本。 大多不含 BI 项目模板。 使用上面的链接可获得正确的版本。 如果你看到 "商业智能项目模板" 文件夹，你将知道 SSDT-BI 的版本是否正确。 此文件夹包含 Analysis Services、Reporting Services 和 Integration Services 的项目模板。 根据安装 SSDT-BI 的方式，可能还会看到一个 SQL Server 数据库项目模板。

 ![SSDT 中新的项目模板](media/ssdt-biprojects.png "SSDT 中新的项目模板")

## <a name="features-recently-added-power-view-for-multidimensional-models"></a>最近添加的功能：用于多维模型的 Power View
 针对多维模型创建 Power View 报表的功能最先是在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 1 累积更新 4 中引入的。 用于多维模型的 Power View 现在包含在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中。

 **用于多维模型的 Power View 报表**

 ![Power View 报表](media/powerviewreport-wn.gif "Power View 报表")

 此功能通过使多维模型（也称为 OLAP 多维数据集）可以与最新客户端报告工具一起使用，帮助组织最大程度利用现有的 BI 投资。 根据多维模型中的数据类型，用户可以方便地创建各种动态可视化对象，从表和矩阵到气泡图和地理图。 多维模型现在还支持使用数据分析表达式 (DAX) 进行查询。

 用于多维模型的 Power View 需要 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的内置 Power View 报告功能（在 SharePoint 模式下）。 其他版本的 Power View（特别是 Excel 2013 中的 Power View 外接程序）不支持多维模型。

 若要了解详细信息，请参阅[多维模型的 Power View](https://msdn.microsoft.com/library/dn140246.aspx)。


