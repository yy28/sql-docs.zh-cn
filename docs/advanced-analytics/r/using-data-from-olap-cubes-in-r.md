---
title: 在 R 中使用 OLAP 多维数据集中的数据
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3063758e1186dc81e5ce9e70891403e7afd3a89f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345109"
---
# <a name="using-data-from-olap-cubes-in-r"></a>在 R 中使用 OLAP 多维数据集中的数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**OlapR**包是由 Microsoft 提供的、用于 Machine Learning Server 和 SQL Server 的 R 包, 可让你运行 MDX 查询从 OLAP 多维数据集获取数据。 对于此包, 无需创建链接服务器或清理平展行集;您可以直接从 R 获取 OLAP 数据。

本文介绍了 API, 并概述了适用于多维数据集数据库的其他用户的 OLAP 和 MDX。

> [!IMPORTANT]
> Analysis Services 的实例可以支持常规多维数据集或表格模型, 但实例不能同时支持这两种类型的模型。 因此, 在尝试生成针对多维数据集的 MDX 查询之前, 请验证 Analysis Services 实例是否包含多维模型。

## <a name="what-is-an-olap-cube"></a>什么是 OLAP 多维数据集？

OLAP 是联机分析处理的简短。 OLAP 解决方案广泛用于随着时间的推移捕获和存储重要的业务数据。 通过多种工具、仪表板和可视化效果将 OLAP 数据用于业务分析。 有关详细信息, 请参阅[联机分析处理](https://en.wikipedia.org/wiki/Online_analytical_processing)。

Microsoft 提供[Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), 这使您能够以_多维数据集_或_表格模型_的形式设计、部署和查询 OLAP 数据。 多维数据集是多维数据库。 _维度_与数据的方面或 R 中的因素类似: 使用维度标识您要汇总或分析的某些特定数据子集。 例如, time 是一个重要维度, 因此很多 OLAP 解决方案都包含默认情况下定义的多个日历, 以便在切片和汇总数据时使用。 

出于性能方面的考虑, OLAP 数据库会提前计算汇总 (或_聚合_), 然后将其存储起来以实现更快的检索。 汇总基于*度量值, 这些度量值*可应用于数值数据。 您可以使用维度来定义数据子集, 然后计算该数据的度量值。 例如, 您可以使用一个度量值计算出多个季度减去税费的某个产品线的总销售额, 以报告特定供应商、本年迄今累积工资支付的平均发货成本等。

多维数据集的 MDX (多维表达式) 是用于查询多维数据集的语言。 MDX 查询通常包含一个数据定义, 其中包含一个或多个维度, 并且至少有一个度量值, 不过, MDX 查询会变得更加复杂, 包括滚动窗口、累计平均值、求和、排名或百分位数。 

下面是开始构建 MDX 查询时可能会有所帮助的其他一些术语:

+ *切片*使用单个维度中的值获取多维数据集的子集。

+ 通过指定多个维度上值的范围，“切块”  创建子多维数据集。

+ “向下钻取”  从摘要导航到详细信息。

+ “向上钻取”  从详细信息移动到较高级别的聚合。

+ “汇总”  总结某个维度上的数据。

+ “透视”  旋转多维数据集或数据选择。

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>如何使用 olapR 创建 MDX 查询

以下文章提供了针对多维数据集创建或执行查询的语法的详细示例:

+ [如何使用 R 创建 MDX 查询](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

**olapR** 包支持两种创建 MDX 查询的方法：

- **使用 MDX 生成器。** 使用包中的 R 函数可以生成简单的 MDX 查询, 方法是选择一个多维数据集, 然后设置轴和切片器。 如果您无法访问传统的 OLAP 工具, 或者没有对 MDX 语言的深入了解, 则可以使用此方法来生成有效的 MDX 查询。

    并非所有 MDX 查询都可以使用此方法创建, 因为 MDX 可能很复杂。 但是, 此 API 支持大多数最常见和有用的操作, 包括在 N 维度中的切片、骰子、深化、汇总和透视。

+ **复制-粘贴格式正确的 MDX。** 手动创建并粘贴到任何 MDX 查询中。 如果要重复使用现有的 MDX 查询, 或如果要生成的查询太复杂, **olapR**无法处理, 则此选项是最佳选择。

    使用任何客户端实用工具 (如 SSMS 或 Excel) 构建 MDX 后, 请保存查询字符串。 将此 MDX 字符串作为参数提供给**olapR**包中的*SSAS 查询处理程序*。 提供程序将查询发送到指定的 Analysis Services 服务器, 并将结果传递回 R。 

有关如何生成 MDX 查询或运行现有 MDX 查询的示例, 请参阅[如何使用 R 创建 mdx 查询](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)。

## <a name="known-issues"></a>已知问题

本部分列出了一些已知问题以及有关**olapR**包的常见问题。

### <a name="tabular-model-support"></a>表格模型支持

如果连接到包含表格模型的 Analysis Services 实例, 则该`explore`函数将报告成功, 返回值为 TRUE。 但是, 表格模型对象不同于多维对象, 而多维数据库的结构不同于表格模型的结构。

尽管 DAX (数据分析表达式) 是通常用于表格模型的语言, 但如果您已熟悉 MDX, 则可以对表格模型设计有效的 MDX 查询。 不能使用 olapR 构造函数来生成针对表格模型的有效 MDX 查询。

但是, MDX 查询是从表格模型检索数据的一种低效的方法。 如果需要从表格模型获取数据以便在 R 中使用, 请考虑以下方法:

+ 对模型启用 DirectQuery, 并将服务器作为链接服务器添加到 SQL Server 中。 
+ 如果表格模型是在关系数据市场上构建的, 则直接从源获取数据。

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>如何确定实例是否包含表格模型或多维模型

单个 Analysis Services 实例只能包含一种类型的模型, 但它可以包含多个模型。 原因在于, 表格模型和多维模型之间存在基本差异, 它们控制数据的存储和处理方式。 例如, 表格模型存储在内存中, 利用列存储索引执行非常快速的计算。 在多维模型中, 数据存储在磁盘上, 并且将提前定义聚合, 并使用 MDX 查询来检索聚合。

如果使用 SQL Server Management Studio 等客户端连接到 Analysis Services, 则可以通过查看数据库的图标来一目了然地支持哪种模型类型。

您还可以查看和查询服务器属性, 以确定实例支持的模型类型。 **服务器模式**属性支持两个值:_多维_或_表格_。

有关这两种模型类型的一般信息, 请参阅以下文章:

+ [比较多维模型和表格模型](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

有关查询服务器属性的信息, 请参阅以下文章:

+ [OLE DB for OLAP 架构行集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>不支持写回

不能将自定义 R 计算的结果写回多维数据集。

通常, 即使为写回启用了多维数据集, 仅支持有限的操作, 并且可能还需要进行其他配置。 建议使用 MDX 进行此类操作。

+ [启用写功能的维度](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [启用写入的分区](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [设置对单元数据的自定义访问权限](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>长时间运行的 MDX 查询块处理多维数据集

尽管**olapR**包仅执行读取操作, 但长时间运行的 MDX 查询可以创建阻止处理多维数据集的锁。 应提前测试 MDX 查询, 以便了解应返回的数据量。

如果尝试连接到锁定的多维数据集, 则可能会收到一个错误, 指出无法访问 SQL Server 数据仓库。 建议的解决方法包括启用远程连接、检查服务器名称或实例名称, 等等。不过, 请考虑先前打开连接的可能性。

SSAS 管理员可以通过标识和终止打开的会话来防止锁定问题。 在服务器级别, 还可以将超时属性应用于 MDX 查询, 以强制终止所有长时间运行的查询。

## <a name="resources"></a>资源

如果不熟悉 OLAP 或 MDX 查询, 请参阅以下维基百科文章: 

+ [OLAP 多维数据集](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX 查询](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
