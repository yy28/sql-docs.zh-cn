---
title: "在 R 中使用来自 OLAP 多维数据集的数据 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# 在 R 中使用来自 OLAP 多维数据集的数据

**olapR** 包是 Microsoft R Server 和 SQL Server R 服务中新提供的 R 包，通过此包，可运行 MDX 查询并在 R 解决方案中使用来自 OLAP 多维数据集的数据。

通过此包，无需创建链接的服务器或清除平展行集；可在 R 中直接使用 OLAP 数据。

## <a name="overview"></a>概述

OLAP 多维数据集是一个包含针对度量值的预计算聚合的多维数据集，它通常捕获重要的业务指标，如销量、销售统计或其他数值。 一直以来，OLAP 多维数据集广泛用于捕获和存储重要的业务数据。 通过多种工具、仪表板和可视化效果将 OLAP 数据用于业务分析。 有关详细信息，请参阅[联机分析处理](https://en.wikipedia.org/wiki/Online_analytical_processing)

**olapR** 包支持两种创建 MDX 查询的方法： 

- 可通过使用 R 样式的 API 选择多维数据集、轴和切片器，生成简单的 MDX 查询。 通过使用这些函数，可创建有效的 MDX 查询，即使不能使用传统 OLAP 工具或没有对 MDX 语言的深入了解，也是如此。

  请注意，通过使用 **olapR** 包中的这一方法，并不能创建所有可能的 MDX 查询，因为 MDX 非常复杂。 但是，它支持所有最常见和有用的操作，包括在 N 维度中切片、切块、向下钻取、汇总和透视。

+ 可手动创建，然后在任何 MDX 查询中粘贴。 如果有要重新使用的现有 MDX 查询，或如果要构建的查询对于 **olapR** 而言处理太过复杂，则此选项很有用。 

  通过此方法，可使用任何客户端实用程序（如 SSMS 或 Excel）构建 MDX，然后将其作为字符串参数用于此包提供的 SSAS 查询处理程序。 **olapR** 函数会将此查询发送到指定的 Analysis Services 服务器，然后将结果传递回 R。

有关如何构建 MDX 查询并运行现有 MDX 查询的示例，请参阅[如何使用 R 创建 MDX 查询](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)。


## <a name="mdx-basics"></a>MDX 基础知识

可以使用 MDX（多维表达式）查询语言检索多维数据集中的数据。 因为 OLAP 多维数据集（或 Analysis Services 数据库）中的数据是多维数据，而不是表格数据，所以 MDX 支持复杂语法和各种操作，对数据进行筛选和切片：

+ 通过选取一个维度的值，“切片”采用多维数据集的一个子集，从而产生小一个维度的多维数据集。 

+ 通过指定多个维度上值的范围，“切块”创建子多维数据集。

+ “向下钻取”从摘要导航到详细信息。

+ “向上钻取”从详细信息移动到较高级别的聚合。

+ “汇总”总结某个维度上的数据。

+ “透视”旋转多维数据集或数据选择。

本主题提供有关显示查询多维数据集的基本语法的更多示例。
[如何使用 R 创建 MDX 查询](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)


## <a name="known-issues"></a>已知问题

### <a name="tabular-models-not-supported-currently"></a>当前不支持表格模型

可连接到 Analysis Services 的表格实例，`explore` 函数将通过返回值 TRUE 报告成功，但表格模型对象不是兼容的类型且无法进行浏览。 

表格模型支持 MDX 查询，但针对表格模型的有效 MDX 查询将返回 NULL 结果并不报告错误。

## <a name="resources"></a>Resources

如果不熟悉 OLAP 或 MDX 查询，请参阅以下 Wikipedia 文章：[OLAP 多维数据集](https://en.wikipedia.org/wiki/OLAP_cube)
[MDX 查询](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)

### <a name="samples"></a>示例

如果想要了解有关多维数据集的详细信息，可以参考 Analysis Services 教程第 4 课[创建 OLAP 多维数据集](https://msdn.microsoft.com/library/ms170208.aspx)，创建用在这些示例中的多维数据集

还可将现有多维数据集作为备份下载，然后将其还原为 Analysis Services 的实例。 例如，可下载 [Adventure Works Multidimensional Model SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334) 的完全处理多维数据集（压缩格式），并将其还原为 SSAS 实例。 有关详细信息，请参阅[备份和还原](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)或 [Restore-ASDatabase Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)。

## <a name="see-also"></a>另请参阅
[如何使用 R 创建 MDX 查询](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)

[适用于 Analysis Services 的 MDX 查询设计器](Analysis%20Services%20MDX%20Query%20Designer%20User%20Interface%20\(Report%20Builder\).md)

