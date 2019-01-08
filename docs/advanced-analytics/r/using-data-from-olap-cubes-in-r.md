---
title: 在 R 的 SQL Server 机器学习服务中使用来自 OLAP 多维数据集的数据
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 347698d2df937b7b64c941ceac81906dcaabbeae
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432630"
---
# <a name="using-data-from-olap-cubes-in-r"></a>在 R 中使用来自 OLAP 多维数据集的数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**OlapR**提供由 Microsoft Machine Learning Server 和 SQL Server 使用的这样，您运行 MDX 查询以从 OLAP 多维数据集获取数据，包，R 包。 通过此包，无需创建链接的服务器或清除平展行集;你可以获取 OLAP 数据直接从。

本文介绍了 API，面向 R 用户可能是刚接触多维数据集数据库的 OLAP 和 MDX 的概述。

> [!IMPORTANT]
> Analysis Services 的实例可以支持传统多维数据集或表格模型中，但实例不能支持这两种类型的模型。 因此，在尝试生成针对多维数据集的 MDX 查询之前，请验证 Analysis Services 实例，包含多维模型。

## <a name="what-is-an-olap-cube"></a>什么是 OLAP 多维数据集？

OLAP 是短，无法用于联机分析处理。 OLAP 解决方案广泛用于捕获和随着时间的推移存储关键业务数据。 通过多种工具、仪表板和可视化效果将 OLAP 数据用于业务分析。 有关详细信息，请参阅[联机分析处理](https://en.wikipedia.org/wiki/Online_analytical_processing)。

Microsoft 提供了[Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services)，它可让你设计、 部署和查询的窗体中的 OLAP 数据_多维数据集_或_表格模型_。 多维数据集是多维数据库。 _维度_等方面的数据或进行了一一对应： 的因素是维度用于标识你想要汇总或分析的数据的某些特定子集。 例如，时间是重要维度，则会为这么多，使许多 OLAP 解决方案包含多个定义的默认情况下，切片和汇总数据时要使用的日历。 

出于性能原因，OLAP 数据库通常计算摘要 (或_聚合_) 预先，然后将其存储的更快地检索。 基于摘要*度量值*，这表示可应用于数值数据的公式。 使用维度来定义数据的子集，然后对这些数据计算度量值。 例如，将使用度量值来计算特定产品系列的总销售额减去税费，若要报告的特定供应商、 年度截止到现在累积工资支付，等的平均装运成本的多个季度内。

MDX 中，多维表达式的缩写，是用于查询多维数据集使用的语言。 MDX 查询通常包含数据定义包含一个或多个维度和至少一个度量值，尽管 MDX 查询可以获取要复杂得多，并将滚动 windows、 累计平均值、 总和、 评级、 或百分位数。 

下面是在启动生成 MDX 查询时可能会有所帮助的一些其他术语：

+ *切片*是通过使用来自单个维度的值，采用多维数据集的子集。

+ 通过指定多个维度上值的范围，“切块”创建子多维数据集。

+ “向下钻取”从摘要导航到详细信息。

+ “向上钻取”从详细信息移动到较高级别的聚合。

+ “汇总”总结某个维度上的数据。

+ “透视”旋转多维数据集或数据选择。

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>如何使用 olapR 创建 MDX 查询

以下文章提供了用于创建或执行针对多维数据集的查询语法的详细的示例：

+ [如何创建使用 R 的 MDX 查询](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

**olapR** 包支持两种创建 MDX 查询的方法：

- **使用 MDX 生成器。** 使用包中的 R 函数生成一个简单的 MDX 查询，通过选择多维数据集，然后再设置轴和切片器。 这是一种生成有效的 MDX 查询，如果您没有使用传统 OLAP 工具，或者没有深入了解 MDX 语言的简便方法。

    可以通过使用此方法中，创建并不是所有 MDX 查询，因为 MDX 可能很复杂。 但是，此 API 支持的大多数最常见和有用的操作，包括在 N 维度中切片、 切块、 向下钻取、 汇总和透视。

+ **复制-粘贴格式正确的 MDX。** 手动创建，然后粘贴在任何 MDX 查询中。 如果您有现有 MDX 查询你想要重复使用，或者如果你想要生成的查询太过复杂，此选项是最好**olapR**来处理。

    构建使用任何客户端实用工具，如 SSMS 或 Excel，在 MDX 后保存的查询字符串。 此 MDX 字符串作为参数提供*SSAS 查询处理程序*中**olapR**包。 提供程序会将查询发送到指定的 Analysis Services 服务器，并将结果传递回。 

有关如何构建 MDX 的示例查询，或运行现有 MDX 查询，请参阅[如何创建使用 R 的 MDX 查询](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)。

## <a name="known-issues"></a>已知问题

本部分列出了一些已知的问题和常见的问题有关**olapR**包。

### <a name="tabular-model-support"></a>表格模型支持

如果连接到的包含表格模型中，Analysis services 实例`explore`函数将报告成功，返回值为 TRUE。 但是，表格模型对象是不同于多维对象和多维数据库的结构是不同的表格模型。

尽管 DAX （数据分析表达式） 是通常与表格模型一起使用的语言，但您可以设计有效的 MDX 查询针对表格模型中，如果你已了解如何使用 MDX。 您不能使用 olapR 构造函数生成有效的 MDX 查询针对表格模型。

但是，MDX 查询是低效的方式来从表格模型检索数据。 如果你需要在 R 中使用表格模型中获取数据，请改为考虑以下方法：

+ 对模型启用 DirectQuery，并将服务器添加为链接服务器在 SQL Server。 
+ 如果表格模型基于关系数据市场，直接从源中获取数据。

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>如何确定实例是否包含表格或多维模型

单个 Analysis Services 实例可以包含模型中，只有一种的类型，但它可以包含多个模型。 原因是表格模型和控制的方式存储和处理数据的多维模型的基本区别。 例如，表格模型存储在内存中，并利用列存储索引以执行非常快计算。 在多维模型中，数据存储在磁盘上和聚合是预先定义和使用 MDX 查询来检索。

如果您连接到 Analysis Services 使用 SQL Server Management Studio 等客户端，可以告诉一眼支持哪种模型类型，通过查看数据库的图标。

您还可以查看和查询来确定哪种类型的模型实例支持的服务器属性。 **服务器模式**属性支持两个值：_多维_或_表格_。

请参阅以下文章了解有关两种类型的模型的常规信息：

+ [多维和表格模型比较](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

请参阅以下文章了解有关查询服务器属性的信息：

+ [OLE DB for OLAP 架构行集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>不支持写回

不能将自定义 R 计算的结果写回到多维数据集。

一般情况下，即使写回启用了多维数据集，支持仅有限的操作，并可能需要其他配置。 我们建议为此类操作使用 MDX。

+ [启用写操作的维度](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [启用写操作的分区](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [设置对单元数据的自定义访问](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>长时间运行的 MDX 查询阻止多维数据集处理

尽管**olapR**包执行只读的操作，运行时间较长的 MDX 查询可以创建阻止从正在处理多维数据集的锁。 始终测试 MDX 查询提前，以便您知道应返回多少数据。

如果你尝试连接到已锁定的多维数据集，可能会收到一个错误，无法访问 SQL Server 数据仓库。 建议的解决方法包括启用远程连接，检查服务器或实例名称等;但是，考虑以前的打开连接的可能性。

SSAS 管理员可阻止通过识别和终止打开的会话锁定问题。 此外可以在服务器级别来强制终止长时间运行的所有查询的 MDX 查询应用一个超时属性。

## <a name="resources"></a>资源

如果您不熟悉 OLAP 或 MDX 查询，请参阅以下 Wikipedia 文章： 

+ [OLAP 多维数据集](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX 查询](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
