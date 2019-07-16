---
title: 如何在 R 中使用 olapR-SQL Server 机器学习服务创建 MDX 查询
description: 使用 SQL Server 中的 olapR 包库 R 语言脚本中编写 MDX 查询。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 66604e44d714837ec9b974af5d0a29b56396cb45
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962641"
---
# <a name="how-to-create-mdx-queries-in-r-using-olapr"></a>如何在 R 中使用 olapR 创建 MDX 查询
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[OlapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)包支持针对托管在 SQL Server Analysis Services 多维数据集的 MDX 查询。 可以生成针对现有的多维数据集的查询、 浏览的维度和多维数据集的其他对象，并粘贴现有 MDX 查询以检索数据中。

本文介绍的两个主要用途**olapR**包：

+ [从 R 使用 olapR 包中提供的构造函数生成的 MDX 查询](#buildMDX)
+ [执行现有的有效 MDX 查询使用 olapR 和 OLAP 访问接口](#executeMDX)

不支持以下操作：

+ 针对表格模型的 DAX 查询
+ 创建新的 OLAP 对象
+ 写回分区，包括度量值或求和

## <a name="buildMDX"></a> 从 R 生成 MDX 查询

1. 定义指定 OLAP 数据源（SSAS 实例）和 MSOLAP 提供程序的连接字符串。

2. 使用函数 `OlapConnection(connectionString)` 创建 MDX 查询的句柄并传递连接字符串。

3. 使用 `Query()` 构造函数实例化查询对象。

4. 使用以下帮助程序函数，提供要包含在 MDX 查询中的维度和度量值的相关详细信息：

     + `cube()` 指定 SSAS 数据库的名称。 如果连接到命名实例，请提供计算机名称和实例名称。 
     + `columns()` 提供要在中使用的度量值的名称**ON COLUMNS**参数。
     + `rows()` 提供要在中使用的度量值的名称**ON ROWS**参数。
     + `slicers()` 指定要作为切片器使用的字段或成员。 切片器就像应用于所有 MDX 查询数据的筛选器一样。
     
     + `axis()` 指定要在查询中使用的附加轴的名称。 
     
         OLAP 多维数据集最多可以包含 128 个查询轴。 通常情况下前, 四个轴称为**列**，**行**，**页**，以及**章节**。 
         
         如果查询相对简单，可以使用函数 `columns`、 `rows`等生成查询。 但也可以使用带非零索引值的 `axis()` 函数，生成具有许多限定符的 MDX 查询或将额外维度添加为限定符。

5. 将句柄，并已完成的 MDX 查询，传递到的以下函数，具体取决于结果的形状之一： 

  + `executeMD` 返回多维数组
  + `execute2D` 返回二维（表格）数据帧

## <a name="executeMDX"></a> 从 R 执行有效的 MDX 查询

1. 定义指定 OLAP 数据源（SSAS 实例）和 MSOLAP 提供程序的连接字符串。

2. 使用函数 `OlapConnection(connectionString)` 创建 MDX 查询的句柄并传递连接字符串。

3. 定义 R 变量来存储 MDX 查询的文本。

4. 将包含 MDX 查询的句柄和变量传递到函数 `executeMD` 或 `execute2D`，具体取决于结果的外观。

    + `executeMD` 返回多维数组
    + `execute2D` 返回二维（表格）数据帧

## <a name="examples"></a>示例

下面的示例基于 AdventureWorks 数据市场和多维数据集项目，因为该项目是广泛可用，在多个版本中，包括可轻松地将还原到 Analysis Services 的备份文件。 如果没有现有的多维数据集，获取示例多维数据集使用这些选项之一：

+ 创建多维数据集，可在这些示例中的 Analysis Services 教程第 4 课：[创建的 OLAP 多维数据集](../../analysis-services/multidimensional-tutorial/multidimensional-modeling-adventure-works-tutorial.md)

+ 下载为备份，将现有多维数据集并将其还原到的 Analysis Services 实例。 例如，此站点提供了完全处理的多维数据集，以压缩格式：[Adventure Works 多维模型 SQL 2014](https://msftdbprodsamples.codeplex.com/downloads/get/882334)。 提取文件，并再将其还原为 SSAS 实例。 有关详细信息，请参阅[备份和还原](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)，或[Restore-asdatabase Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)。

### <a name="1-basic-mdx-with-slicer"></a>1.带切片器的基本 MDX

此 MDX 查询将选择度量值  ，用于 Internet 销售计数和销量的计数和数量，并将它们放置到“列”轴。 它将 SalesTerritory 维度的成员添加为切片器  来筛选查询，使计算中仅使用澳大利亚的销售额。

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, 
{[Product].[Product Line].[Product Line].MEMBERS} ON ROWS 
FROM [Analysis Services Tutorial] 
WHERE [Sales Territory].[Sales Territory Country].[Australia]
```

+ 在列上可将多个度量值指定为逗号分隔字符串的元素。
+ “行”轴使用“产品系列”维度的所有可能的值（所有成员）。 
+ 此查询将返回一个表包含三列，其中包含_汇总_摘要的所有国家/地区的 Internet 销售额。
+ WHERE 子句指定_切片器轴_。 在此示例中，切片器使用的成员**SalesTerritory**维度来筛选查询，以便在计算中使用仅从澳大利亚的销售额。

#### <a name="to-build-this-query-using-the-functions-provided-in-olapr"></a>使用 olapR 中提供的函数生成此查询

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)

qry <- Query()
cube(qry) <- "[Analysis Services Tutorial]"
columns(qry) <- c("[Measures].[Internet Sales Count]", "[Measures].[Internet Sales-Sales Amount]")
rows(qry) <- c("[Product].[Product Line].[Product Line].MEMBERS") 
slicers(qry) <- c("[Sales Territory].[Sales Territory Country].[Australia]")

result1 <- executeMD(ocs, qry)

```

对于命名实例，请确保任何被视为在 R 中的控制字符的字符进行转义 例如，以下连接字符串引用实例 OLAP01，名为 ContosoHQ 的服务器上：

```R
cnnstr <- "Data Source=ContosoHQ\\OLAP01; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
```

#### <a name="to-run-this-query-as-a-predefined-mdx-string"></a>将此查询作为预定义的 MDX 字符串运行

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)

mdx <- "SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, {[Product].[Product Line].[Product Line].MEMBERS} ON ROWS FROM [Analysis Services Tutorial] WHERE [Sales Territory].[Sales Territory Country].[Australia]"

result2 <- execute2D(ocs, mdx)
```

如果您在 SQL Server Management Studio 中使用 MDX 生成器定义查询，然后保存 MDX 字符串，它将从 0，开始为轴编号，如下所示： 

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Countr,y].[Australia]
```

仍可将此查询作为预定义的 MDX 字符串运行。 但是，若要生成相同的查询使用 R 使用`axis()`函数，您必须重新编号从 1 开始的轴。

### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2.浏览 SSAS 实例上的多维数据集及其字段

可以使用 `explore` 函数返回要用于构造查询的多维数据集、 维度或成员的列表。 如果无法使用其他 OLAP 浏览工具，或要通过编程方式操作或构造 MDX 查询，这非常方便。

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>列出指定连接上可用的多维数据集

若要查看有权查看的实例上的所有多维数据集或透视，将句柄作为 `explore`的参数提供。

> [!IMPORTANT]
> 最终结果是**不**多维数据集;TRUE 仅表示元数据操作是否成功。 如果参数无效，将引发错误。

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)
explore(ocs)
```

| 结果  |
| ----|
| Analysis Services 教程 |
|Internet 销售额 |
|分销商销售额 |
|销售汇总 |
|[1] TRUE |

#### <a name="to-get-a-list-of-cube-dimensions"></a>获取多维数据集维度列表

若要查看多维数据集或透视中的所有维度，请指定多维数据集或透视名称。

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs \<- OlapConnection(cnnstr)
explore(ocs, "Sales")
```

| 结果  |
| ----|
| 客户 |
|日期 |
|地区 |


#### <a name="to-return-all-members-of-the-specified-dimension-and-hierarchy"></a>返回指定维度和层次结构的所有成员

定义源并创建句柄后，指定要返回的多维数据集、维度和层次结构。 在返回的结果中，带有前缀的项 **->** 表示上一个成员的子级。

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)
explore(ocs, "Analysis Services Tutorial", "Product", "Product Categories", "Category")
```

| 结果  |
| ----|
| 附件 |
|自行车 |
|服装 |
|_组件_|
|-> 程序集组件|
|-> 程序集组件|


## <a name="see-also"></a>请参阅

[在 R 中使用来自 OLAP 多维数据集的数据](../../advanced-analytics/r/using-data-from-olap-cubes-in-r.md)
