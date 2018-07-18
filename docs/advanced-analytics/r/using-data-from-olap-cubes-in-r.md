---
title: 使用 OLAP 多维数据集数据中 R （SQL Server 机器学习） |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0753fc84ea6516da63e1e49dc68063780b99361b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203689"
---
# <a name="using-data-from-olap-cubes-in-r"></a>在 R 中使用来自 OLAP 多维数据集的数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**OlapR**包是一个 R 程序包时，提供用于机器学习 Server 和 SQL Server 的 microsoft，它允许你运行 MDX 查询以从 OLAP 多维数据集获取数据。 此程序包，你不需要创建链接的服务器或清理平展行集;你可以获取 OLAP 数据直接从。

本文介绍的 API，以及为这些用户可能不熟悉多维数据集数据库 R 用户 OLAP 和 MDX 的概述。

> [!IMPORTANT]
> Analysis Services 的实例可以支持常规多维数据集或表格模型中，但实例不能支持两种类型的模型。 因此，你尝试生成针对多维数据集的 MDX 查询之前，请验证 Analysis Services 实例，包含多维模型。

## <a name="what-is-an-olap-cube"></a>什么是 OLAP 多维数据集？

OLAP 是短，无法用于联机分析处理。 OLAP 解决方案广泛用于捕获和随着时间的推移存储关键业务数据。 通过多种工具、仪表板和可视化效果将 OLAP 数据用于业务分析。 有关详细信息，请参阅[联机分析处理](https://en.wikipedia.org/wiki/Online_analytical_processing)。

Microsoft 提供了[Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services)，它可让你设计、 部署和查询中的窗体的 OLAP 数据_多维数据集_或_表格模型_。 多维数据集是多维数据库。 _维度_等方面的数据或在： 的因素是你使用维度来标识你想要汇总或分析的数据的某些特定子集。 例如，时间是重要维度，则会为太多，使许多 OLAP 解决方案包含多个定义默认情况下，进行切片和汇总数据时要使用的日历。 

出于性能原因，OLAP 数据库通常计算摘要 (或_聚合_) 提前，然后将其存储进行更快地检索。 摘要基于*度量值*，分别表示可应用于数值数据的公式。 使用维度定义的数据子集，然后对该数据计算度量值。 例如，你将使用度量值计算税收，以报告特定供应商、 年度截止到现在累积工资支付，等的平均传送成本减去的多个季度的某些产品系列的总销售额。

MDX，短的多维表达式，是用于查询多维数据集的语言。 MDX 查询通常包含包含一个或多个维度和至少一个度量值，但 MDX 查询可以获取复杂得多，并包含滚动窗口、 累计平均值、 sum、 排名或百评分的数据定义。 

以下是当你开始生成 MDX 查询时，可能很有帮助的一些其他词：

+ *进行切片*通过使用来自单个维度的值，采用该多维数据集的子集。

+ 通过指定多个维度上值的范围，“切块”创建子多维数据集。

+ “向下钻取”从摘要导航到详细信息。

+ “向上钻取”从详细信息移动到较高级别的聚合。

+ “汇总”总结某个维度上的数据。

+ “透视”旋转多维数据集或数据选择。

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>如何使用 olapR 创建 MDX 查询

以下文章提供了用于创建或对多维数据集执行查询的语法的详细的示例：

+ [如何创建使用 R 的 MDX 查询](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

**olapR** 包支持两种创建 MDX 查询的方法：

- **使用 MDX 生成器。** 使用包中的 R 函数来生成简单的 MDX 查询，通过选择多维数据集，然后再设置轴和切片器。 这是轻松生成有效的 MDX 查询，如果您没有访问传统 OLAP 工具，或者没有了解 MDX 语言的深入知识。

    可以通过使用此方法，创建不是所有 MDX 查询，因为 MDX 可以很复杂。 但是，此 API 支持的最常见和有用的操作，包括 N 维度中的切片、 切块、 深化、 rollup 和透视的大部分。

+ **复制和粘贴格式正确的 MDX。** 手动创建，然后粘贴在所有 MDX 查询中。 此选项是最佳，如果你有现有的 MDX 查询你想要重复使用，或者如果你想要生成的查询太过复杂， **olapR**来处理。

    生成使用任何客户端实用工具，如 SSMS 或 Excel，你 MDX 后保存的查询字符串。 提供此 MDX 字符串的自变量作为*SSAS 查询处理程序*中**olapR**包。 提供将查询发送到指定的 Analysis Services 服务器，并将结果传递回。 

有关如何生成 MDX 的示例查询，或运行现有 MDX 查询，请参阅[如何创建使用 R 的 MDX 查询](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)。

## <a name="known-issues"></a>已知问题

本部分列出了一些已知的问题和常见问题有关**olapR**包。

### <a name="tabular-model-support"></a>表格模型支持

如果你连接到包含表格模型的 Analysis Services 的实例`explore`函数报告成功并返回值为 TRUE。 但是，表格模型对象与多维对象不同，多维数据库的结构是不同的表格模型。

尽管 DAX （数据分析表达式） 是通常与表格模型使用的语言，你可以设计有效的 MDX 查询针对表格模型中，如果你已了解如何使用 MDX。 不能使用 olapR 构造函数来生成有效的 MDX 查询针对表格模型。

但是，MDX 查询是从表格模型检索数据的效率低下方法。 如果你需要在 R 中使用从表格模型获取数据，请改为考虑以下方法：

+ 对模型启用 DirectQuery 和将服务器添加为 SQL Server 中的链接服务器。 
+ 如果关系的数据市场上生成表格模型时，请直接从源获取数据。

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>如何确定实例是否包含表格或多维模型

单个 Analysis Services 实例可以包含模型，只有一个的类型，但它可以包含多个模型。 原因是表格模型和控制的方式存储和处理数据的多维模型之间的基本差异。 例如，表格模型存储在内存中，并利用列存储索引来执行非常快速地计算。 在多维模型中，数据存储在磁盘上并聚合是预先定义和使用 MDX 查询中检索。

如果你连接到 Analysis Services 使用 SQL Server Management Studio 等客户端，可让一眼支持哪种模型类型，通过查看数据库的图标。

你还可以查看和查询以确定哪种类型的模型该实例支持的服务器属性。 **服务器模式**属性支持两个值：_多维_或_表格_。

请参阅以下文章有关模型的两种类型的常规信息：

+ [比较多维和表格模型](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

请参阅以下文章了解有关查询服务器属性：

+ [OLE DB for OLAP 架构行集](https://docs.microsoft.com/sql/analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>不支持写回

不能将自定义 R 计算的结果写回到该多维数据集。

一般情况下，即使写回功能启用了多维数据集，支持仅有限的操作，并可能需要其他配置。 我们建议你执行诸如操作使用 MDX。

+ [写入的维度](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [写入的分区](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [设置对单元数据的自定义的访问](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>长时间运行 MDX 查询阻止多维数据集处理

尽管**olapR**包执行仅读的操作，可长时间运行 MDX 查询可以创建阻止从正在处理多维数据集的锁。 始终测试 MDX 查询提前，以便你知道应返回的数据量。

如果你尝试连接到已锁定的多维数据集，你可能会无法访问 SQL Server 数据仓库的错误。 建议的解决方法包括启用远程连接，检查的服务器或实例名称和等;但是，请考虑以前的打开连接的可能性。

SSAS 管理员可阻止通过识别并终止打开的会话锁定问题。 超时属性也可以应用于在服务器级别强制终止的长时间运行的所有查询的 MDX 查询。

## <a name="resources"></a>Resources

如果你不熟悉到 OLAP 或 MDX 查询，请参阅以下 Wikipedia 文章： 

+ [OLAP 多维数据集](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX 查询](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
