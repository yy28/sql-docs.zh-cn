---
title: "下载 SQL Server Data Tools (SSDT) | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "安装 ssdt, 下载 ssdt, 最新 ssdt"
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 681ad2f6d7aeb88db45dde3f2e695db672b97dbd
ms.lasthandoff: 04/11/2017

---
# <a name="download-sql-server-data-tools-ssdt"></a>下载 SQL Server Data Tools (SSDT)

**[SQL Server Data Tools](https://msdn.microsoft.com/mt186501)** 是一款可免费下载的现代开发工具，用于生成 SQL Server 关系数据库、Azure SQL 数据库、Integration Services 包、Analysis Services 数据模型和 Reporting Services 报表。 使用 SSDT，你可以设计和部署任何 SQL Server 内容类型，就像在 Visual Studio 中开发应用程序一样轻松。 此版本支持 SQL Server 2005 至 SQL Server 2016 并提供用于添加 SQL Server 2016 中的新增功能的设计环境。  
    
    
| ![下载](../ssdt/media/download.png) 下载适用于 Visual Studio 2015 的 SQL Server Data Tools  | 下载数据层应用程序框架 (DacFx) ||
|:---|:---|:---|
|**[下载 SQL Server Data Tools (16.5)](https://msdn.microsoft.com/mt186501)**|[**下载 DacFx 和 SqlPackage.exe (16.5)**](https://www.microsoft.com/download/details.aspx?id=54106) |用于生产的最新 GA 版本。|
|[**下载 SQL Server Data Tools - 候选发布**](../ssdt/sql-server-data-tools-ssdt-release-candidate.md)| [**下载 DacFx 和 SqlPackage.exe - 候选发布**](../ssdt/sql-server-data-tools-ssdt-release-candidate.md) |包括对 SQL Server vNext 的支持。|



## <a name="download-visual-studio"></a>下载 Visual Studio

* [**下载 Visual Studio 社区 2015**](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)

### <a name="use-ssdt-in-visual-studio-2017"></a>在 Visual Studio 2017 中使用 SSDT

* [**下载 Visual Studio 2017**](https://www.visualstudio.com/)（[Visual Studio 2017 各版本的功能比较](https://www.visualstudio.com/vs/compare/)）

若要使用关系数据库项目，建议在安装期间检查**数据存储和处理**工作负载。 其他许多工作负载（包括 *Azure*、*ASP.Net 和 Web 开发*以及 *.Net Core 跨平台开发*）也提供 SSDT 数据库项目支持。

若要结合使用 SSDT 和 Visual Studio 2017，请安装 AS 和 RS 组件：
* [Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)
* [Reporting Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)


## <a name="installing-ssdt-without-visual-studio-pre-installed"></a>在未预安装 Visual Studio 的情况下安装 SSDT

如果未在计算机上安装 Visual Studio，安装适用于 Visual Studio 2015 的 SSDT 将同时安装 Visual Studio 2015 的最低“集成 Shell”版本。 此版本的 Visual Studio 可以在任意多台计算机上免费安装和使用。 它可提供所有 SQL Server 项目类型以及 SQL Server 对象资源管理器和其他 SQL 工具体验。

如果计算机上已安装 [Visual Studio 2015 社区版（或更高版本）](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)，安装 SSDT 时将向现有的 Visual Studio 安装添加完整的 SQL Server 工具。 Visual Studio 包括你可能需要使用的多种功能，例如源代码控制集成和非 SQL 语言支持。 建议使用 Visual Studio 2015 社区版或更高版本，以在开发 T-SQL 时获得最佳体验。

## <a name="supported-sql-versions"></a>受支持的 SQL 版本
  
|项目模板|支持的 SQL 平台|  
|-------------------|--------------------|  
关系数据库|  SQL Server 2005* - SQL Server 2016 <br /><br />Azure SQL Database<br /><br />Azure SQL 数据仓库（仅支持查询；尚不支持数据库项目）<br /><br />  * SQL Server 2005 支持已停止提供，<br /><br /> 请转至官方支持的 SQL 版本|
  |Analysis Services 模型<br /><br />Reporting Services 报表 | SQL Server 2008 – SQL Server 2016|
  |Integration Services 包| SQL Server 2012 – SQL Server 2016    |
  
## <a name="next-steps"></a>后续步骤  
安装 SSDT 后，阅读这些教程，了解如何使用 SSDT 创建数据库、包、数据模型和报告：  
  
-   [面向项目的脱机数据库开发](https://msdn.microsoft.com/library/hh272702(v=vs.103).aspx)  
  
-   [SSIS 教程：创建简单的 ETL 包](https://msdn.microsoft.com/library/ms169917.aspx)  
  
-   [Analysis Services 教程](https://msdn.microsoft.com/library/hh231701.aspx)  
  
-   [创建基本表报表（SSRS 教程）](https://msdn.microsoft.com/library/ms167305.aspx)  
  
## <a name="see-also"></a>另请参阅  
[Visual Studio 中的 SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN 论坛](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 团队博客](http://blogs.msdn.com/b/ssdt/)  
[SSDT Connect 反馈](https://connect.microsoft.com/SQLServer/Feedback)  
[SSDT 文档](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[DACFx API 参考](https://msdn.microsoft.com/library/dn645454.aspx)  
[下载 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  

