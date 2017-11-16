---
title: "已更新 - 关系数据库文档 | Microsoft Docs"
description: "显示关系数据库文档中最近更改的更新内容片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: 
ms.component: relational-databases-misc
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: 
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 70cb071dc7b6f4ff15c5c7dee3f24bb352d6eb61
ms.contentlocale: zh-cn
ms.lasthandoff: 10/02/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>新文章和最近更新的文章：关系数据库文档
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：从 2017-09-11 到 2017-09-27&nbsp;&nbsp;&nbsp;
- 主题领域：&nbsp; 关系数据库。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [在 SQL Server 和 Azure SQL 数据库中导入和导出数据](import-export/overview-import-export.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [空间数据类型概述](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-spatial-data-types-overviewspatialspatial-data-types-overviewmd"></a>1.&nbsp;[空间数据类型概述](spatial/spatial-data-types-overview.md)

更新日期：2017-09-26&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 

<!-- Source markdown line 27.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 96dd44cf49e96d1d543a629d49de297dba9c1753 2e9629f852ea42a213c7c24831bcfa53e40358f2  (PR=0  ,  Filename=spatial-data-types-overview.md  ,  Dirpath=docs\relational-databases\spatial\  ,  MergeCommitSha40=b33976cf92f23fbb13cee0c353fd40608d002d94) -->



 -  有两种类型的空间数据。 **geometry** 数据类型支持平面或欧几里得（平面球）数据。 **geometry** 数据类型符合开放地理空间联盟 (OGC) 的 SQL 简单特征规范 1.1.0 版 并符合 SQL MM（ISO 标准）。
 -
 - 另外，..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 支持 geography 数据类型，该数据类型可存储诸如 GPS 纬度和经度坐标之类的椭圆体（圆球）数据。
 -
 -> [!IMPORTANT]
 -> 有关 ..!NCLUDE-NotShown--ssSQL11--../../includes/sssql11-md.md)] 中引入的空间功能的详细说明和示例（包括对空间数据类型的改进），请下载白皮书 [New Spatial Features in SQL Server Code-Named "Denali"](http://go.microsoft.com/fwlink/?LinkId=226407)（SQL Server Code-Named "Denali" 中的新空间功能）。
 -
 -##  <a name="objects"></a> 空间数据对象
 - **geometry** 和 **geography** 数据类型支持十六种空间数据对象或实例类型。 但是，这些实例类型中只有十一种“可实例化”；可以在数据库中创建并使用这些实例（或可对其进行实例化）。 这些实例的某些属性从其父级数据类型派生而来，使其在 **Points**中区分为 **LineStrings, CircularStrings**、 **CompoundCurves**、 **Polygons**、 **CurvePolygons** 、 **geometry** 或多个 **geography** 或 **GeometryCollection**实例。 **Geography** 类型具有附加实例类型 **FullGlobe**。
 -
 - 下图描述了 **geometry** 和 **geometry** 数据类型所基于的 **geography** 层次结构。 **geometry** 和 **geography** 的可实例化类型以蓝色表示。
 -
 - ![geom_hierarchy--../../relational-databases/spatial/media/geom-hierarchy.gif)
 -
 - 如图所示， **geometry** 和 **geography** 数据类型的十种可实例化类型为 **Point**、 **MultiPoint**、 **LineString**、 **CircularString**、 **MultiLineString**、 **CompoundCurve**、 **Polygon**、 **CurvePolygon**、 **MultiPolygon**和 **GeometryCollection**。 geography 数据类型有一个附加可实例化类型： **FullGlobe**。 只要特定实例的格式正确，即使未显式定义该实例， **geometry** 和 **geography** 类型也可识别该实例。 例如，如果你使用 STPointFromText() 方法显式定义了一个 **Point** 实例，只要方法输入的格式正确， **geometry** 和 **geography** 便将该实例识别为 **Point**。 如果你使用 `STGeomFromText()` 方法定义了相同的实例，则 **geometry** 和 **geography** 数据类型都将该实例识别为 **Point**。







## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新文章和更新的文章 (0+1)：SQL 高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章和更新的文章 (0+1)：SQL Analysis Services 文档](../analysis-services/new-updated-analysis-services.md)
- [新文章和更新的文章 (4+1)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新文章和更新的文章 (17+0)：SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)
- [新文章和更新的文章 (3+0)：Linux for SQL 文档](../linux/new-updated-linux.md)
- [新文章和更新的文章 (1+1)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新文章和更新的文章 (2+0)：SQL Reporting Services 文档](../reporting-services/new-updated-reporting-services.md)
- [新文章和更新的文章 (0+1)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新文章和更新的文章 (0+1)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新文章和更新的文章 (0+0)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../sample/new-updated-sample.md)
- [新文章和更新的文章 (0+0)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新的和更新的文章 (0+0)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新的和更新的文章 (0+0)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新文章和更新的文章 (0+0)：SQL 工具文档](../tools/new-updated-tools.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)



