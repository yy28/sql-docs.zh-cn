---
title: "在 R 中使用来自 OLAP 多维数据集的数据 |Microsoft 文档"
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 1c55a5b834cd91478a87ded7ebb86884117c7bfb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="using-data-from-olap-cubes-in-r"></a>在 R 中使用来自 OLAP 多维数据集的数据

**OlapR**包是一个 R 程序包时，提供用于机器学习服务器和 SQL Server R Services 的 microsoft，它允许你运行 MDX 查询以从 OLAP 多维数据集获取数据。 此程序包，你不需要创建链接的服务器或清理平展行集;你可以使用 OLAP 数据直接中。

本文介绍的 API，以及概述 fo OLAP 和 R 用户这些用户可能不熟悉多维数据集数据库的 MDX。

## <a name="what-is-an-olap-cube"></a>什么是 OLAP 多维数据集？

OLAP 是短，无法用于联机分析处理。 OLAP 解决方案广泛用于捕获和随着时间的推移存储关键业务数据。 通过多种工具、仪表板和可视化效果将 OLAP 数据用于业务分析。 有关详细信息，请参阅[联机分析处理](https://en.wikipedia.org/wiki/Online_analytical_processing)。

Microsoft 提供了[Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services)，它可让你设计、 部署和查询中的窗体的 OLAP 数据_多维数据集_或_表格模型_。 多维数据集是多维数据库。 _维度_等方面的数据或在： 的因素是你使用维度来标识你想要汇总或分析的数据的某些特定子集。 例如，时间是重要维度，则会为太多，使许多 OLAP 解决方案包含多个定义默认情况下，进行切片和汇总数据时要使用的日历。 

出于性能原因，OLAP 数据库通常计算摘要 (或_聚合_) 提前，然后将其存储进行更快地检索。 摘要基于*度量值*，分别表示可应用于数值数据的公式。 使用维度定义的数据子集，然后对该数据计算度量值。 例如，你将使用度量值计算税收，以报告特定供应商、 年度截止到现在累积工资支付，等的平均传送成本减去的多个季度的某些产品系列的总销售额。

MDX，短的多维表达式，是用于查询多维数据集的语言。 MDX 查询通常包含包含一个或多个维度和至少一个度量值的数据定义，获取复杂得多，并包括滚动窗口、 累计平均值或 sum、 百评分 thogh MDX 查询。 

以下是当你开始生成 MDX 查询时，可能很有帮助的一些其他词：

+ *进行切片*通过使用来自单个维度的值，采用该多维数据集的子集。

+ 通过指定多个维度上值的范围，“切块”创建子多维数据集。

+ “向下钻取”从摘要导航到详细信息。

+ “向上钻取”从详细信息移动到较高级别的聚合。

+ “汇总”总结某个维度上的数据。

+ “透视”旋转多维数据集或数据选择。

本主题提供用于多维数据集上的查询的基本语法的更多示例： 

+ [如何创建使用 R 的 MDX 查询](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

**olapR** 包支持两种创建 MDX 查询的方法：

- **使用 MDX 生成器。** 使用包中的 R 函数来生成简单的 MDX 查询，通过选择多维数据集，并设置轴和切片器。 这是轻松生成有效的 MDX 查询，如果您没有访问传统 OLAP 工具，或者没有了解 MDX 语言的深入知识。

    可以通过使用此方法，创建不是所有可能的 MDX 查询，因为 MDX 可以很复杂。 但是，此 API 支持的最常见和有用的操作，包括 N 维度中的切片、 切块、 深化、 rollup 和透视的大部分。

+ **复制和粘贴格式正确的 MDX。** 手动创建，然后粘贴在所有 MDX 查询中。 此选项是最佳，如果你有现有的 MDX 查询你想要重复使用，或者如果你想要生成的查询太过复杂， **olapR**来处理。 

    生成使用任何客户端实用工具，如 SSMS 或 Excel，你 MDX，然后保存定义 MDX 查询的字符串。 你提供此 MDX 字符串的自变量作为*SSAS 查询处理程序*中**olapR**包。 该函数将查询发送到指定的 Analysis Services 服务器，并将结果传递回 R，假设您有权当然查询多维数据集。

有关如何生成 MDX 的示例查询，或运行现有 MDX 查询，请参阅[如何创建使用 R 的 MDX 查询](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)。

## <a name="known-issues"></a>已知问题

### <a name="tabular-models-not-supported"></a>不支持的表格模型

+ 如果你连接到 Analysis Services 的表格实例`explore`函数报告成功并返回值为 TRUE。 但是，表格模型对象不为某个兼容类型，并且无法解决。

+ 可以使用 DAX 或 MDX 查询表格模型。 如果你在设计有效的 MDX 查询针对表格模型使用外部工具，然后将查询粘贴到此 API，查询将返回 NULL 结果，并不会报告错误。

## <a name="resources"></a>Resources

如果不熟悉 OLAP 或 MDX 查询，请参阅以下 Wikipedia 文章： [OLAP 多维数据集](https://en.wikipedia.org/wiki/OLAP_cube)
[MDX 查询](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)

### <a name="samples"></a>示例

如果想要了解有关多维数据集的详细信息，可以参考 Analysis Services 教程第 4 课 [创建 OLAP 多维数据集](../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)，创建用在这些示例中的多维数据集

还可将现有多维数据集作为备份下载，然后将其还原为 Analysis Services 的实例。 例如，可下载 [Adventure Works Multidimensional Model SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334)的完全处理多维数据集（压缩格式），并将其还原为 SSAS 实例。 有关详细信息，请参阅 [备份和还原](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)或 [Restore-ASDatabase Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)。
