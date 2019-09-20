---
title: 使用 R 和 SQL 数据类型和对象
titleSuffix: SQL Server Machine Learning Services
description: 本快速入门介绍如何使用 SQL Server 机器学习服务在 R 和 SQL Server 中使用数据类型和数据对象。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 85bfe26826e6e8ed04579526462babe2b5dcf009
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2019
ms.locfileid: "71149961"
---
# <a name="quickstart-handle-data-types-and-objects-using-r-in-sql-server-machine-learning-services"></a>快速入门：在 SQL Server 中使用 R 处理数据类型和对象机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入门中，你将了解在 R 和 SQL Server 之间移动数据时发生的常见问题。 在此练习中, 您可以在自己的脚本中使用数据时提供基本的背景知识。

提前了解常见问题包括:

- 数据类型有时不匹配
- 可能发生隐式转换
- 有时需要执行强制转换和转换操作
- R 和 SQL 使用不同的数据对象

## <a name="prerequisites"></a>先决条件

- 此快速入门要求使用安装 R 语言的[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)SQL Server 的实例。

  SQL Server 实例可位于 Azure 虚拟机或本地。 请注意，默认情况下禁用外部脚本功能，因此在开始之前，您可能需要[启用外部脚本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并验证**SQL Server Launchpad 服务**是否正在运行。

- 还需要一个用于运行包含 R 脚本的 SQL 查询的工具。 您可以使用任何数据库管理或查询工具运行这些脚本，只要它可以连接到 SQL Server 实例，然后运行 T-sql 查询或存储过程。 本快速入门使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="always-return-a-data-frame"></a>始终返回数据帧

当脚本将结果从 R 返回给 SQL Server 时，必须以 **data.frame** 的形式返回数据。 在脚本中生成的任何其他类型的对象 (无论是列表、系数、矢量还是二进制数据), 如果要在存储过程结果中输出, 则必须将其转换为数据帧。 幸运的是，有多个 R 函数支持将其他对象更改为数据框架。 甚至可以序列化二进制模型，并在数据帧中返回它，稍后会在本快速入门中执行此操作。

首先, 让我们试验一些 R basic R 对象-矢量、矩阵和列表, 并了解转换到数据帧的方式如何更改传递到 SQL Server 的输出。

将 R 中的这两个 "Hello World" 脚本进行比较。脚本看起来几乎完全相同, 但第一列返回三个值中的一个, 而第二个列返回三个列, 每个列都有一个值。

**示例 1**

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
     , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
     , @input_data_1 = N' ';
```

**示例 2**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'
      , @input_data_1 = N'  ';
```

## <a name="identify-schema-and-data-types"></a>标识架构和数据类型

结果为何有这么大的差别？

使用 R `str()` 命令通常可以找到答案。 在 R 脚本中的任何位置添加函数 `str(object_name)` 可使指定 R 对象的数据架构作为信息性消息返回。 若要查看消息，请查看 Visual Studio Code 中的“消息”窗格，或者查看 SSMS 中的“消息”选项卡。

若要找出示例 1 和示例 2 的结果为何有这么大的差别，请在每个语句的 _@script_ 变量定义末尾插入 `str(OutputDataSet)` 行，如下所示：

**添加了 str 函数的示例1**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      OutputDataSet <- as.data.frame(mytextvariable);
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**示例2已添加 str 函数**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet);' , 
  @input_data_1 = N'  ';
```

现在，查看“消息”中的文本，了解输出为何不相同的原因。

**结果 - 示例 1**

```sql
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**结果 - 示例 2**

```sql
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

可以看到，对 R 语法进行轻微的更改会给结果的架构造成很大的影响。 我们不会探讨原因, 但 R 数据类型中的差异在[Hadley Wickham 的 "高级 R" 的 "](http://adv-r.had.co.nz)*数据结构*" 部分的详细信息中进行了介绍。

暂时，你只需在将 R 对象强制转换成数据框架时注意检查预期的结果。

> [!TIP]
> 你还可以使用 R 标识函数 (如`is.matrix`) `is.vector`来返回有关内部数据结构的信息。

## <a name="implicit-conversion-of-data-objects"></a>数据对象的隐式转换

每个 R 数据对象都有自身的规则，指定在将值与其他数据对象组合时，如果两个数据对象具有相同的维度数目，或者如果任意数据对象包含异构数据类型，应如何处理值。

首先，创建一个较小的测试数据表。

```sql
CREATE TABLE RTestData (col1 INT NOT NULL)

INSERT INTO RTestData
VALUES (1);

INSERT INTO RTestData
VALUES (10);

INSERT INTO RTestData
VALUES (100);
GO
```

例如, 假定您运行以下语句来使用 R 执行矩阵乘法。您可以将具有三个值的单列矩阵乘以具有四个值的数组, 并期望4x3 矩阵为结果。

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:15);
    OutputDataSet <- as.data.frame(x %*% y);'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));
```

在幕后，包含三个值的列将转换为单列矩阵。 由于矩阵只是 R 中数组的特殊表示形式，数组 `y` 将隐式强制转换为单列矩阵，使这两个参数相符。

**结果**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|

不过, 请注意更改数组`y`大小时会发生什么情况。

```sql
execute sp_execute_external_script
   @language = N'R'
   , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:14);
   OutputDataSet <- as.data.frame(y %*% x);'
   , @input_data_1 = N' SELECT [Col1]  from RTestData;'
   WITH RESULT SETS (([Col1] int ));
```

现在，R 返回单个值作为结果。

**结果**

|Col1|
|---|
|1542|

原因是什么？ 在这种情况下, 因为这两个参数可以作为相同长度的向量来处理, 所以 R 将内部产品返回为矩阵。  根据线性代数的规则，这种行为符合预期；但是，如果下游应用程序预期输出架构永远不变，则这种行为可能会导致问题！

> [!TIP]
> 
> 出现错误？ 请确保在包含表的数据库的上下文中运行存储过程，而不是在**master**或其他数据库中运行该存储过程。
>
> 此外, 我们建议你避免在这些示例中使用临时表。 某些 R 客户端将终止批处理之间的连接, 从而删除临时表。

## <a name="merge-or-multiply-columns-of-different-length"></a>对不同长度的列进行合并或相乘

R 提供了很大的灵活性, 可以使用不同大小的矢量, 并将这些类似列的结构组合到数据帧中。 向量列表可能看起来像表，但它们并不遵循控制数据库表的所有规则。

例如，以下脚本定义长度为 6 的数字数组，并将其存储在 R 变量 `df1` 中。 然后将该数值数组与包含三 (3) 个值的 RTestData 表的整数组合, 以生成新的数据帧`df2`。

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
               df1 <- as.data.frame( array(1:6) );
               df2 <- as.data.frame( c( InputDataSet , df1 ));
               OutputDataSet <- df2'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));
```

为了填充数据框架，R 将以所需的次数重复从 RTestData 检索的元素，以匹配数组 `df1` 中的元素数目。

**结果**

|*Col2*|*Col3*|
|----|----|
|1|1|
|10|2|
|100|3|
|1|4|
|10|5|
|100|6|

请记住，数据框架只是看起来像表，但实际上是向量列表。

## <a name="cast-or-convert-sql-server-data"></a>强制转换或转换 SQL Server 数据

R 和 SQL Server 使用的数据类型不同，因此，如果你在 SQL Server 中运行查询来获取数据，然后将该数据传递给 R 运行时，通常会发生某种类型的隐式转换。 将数据从 R 返回到 SQL Server 时，会发生另一套转换。

- SQL Server 将查询中的数据推送到快速启动板服务所管理的 R 进程, 并将其转换为内部表示形式以提高效率。
- R 运行时将数据加载到 data.frame 变量中，并对数据执行其自身的操作。
- 数据库引擎使用受保护的内部连接将数据返回到 SQL Server，并以 SQL Server 数据类型呈现数据。
- 若要获取数据，可以使用能够发出 SQL 查询并处理表格数据集的客户端或网络库连接到 SQL Server。 此客户端应用程序可能会通过其他方式影响数据。

若要查看其工作原理, 请在[AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)数据仓库上运行如下查询。 此视图返回用于创建预测的销售数据。

```sql
USE AdventureWorksDW
GO

SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
>
> 您可以使用任何版本的 AdventureWorks, 或使用自己的数据库创建不同的查询。 要点是尝试处理包含文本、日期时间和数字值的某些数据。

现在, 请尝试将此查询作为输入粘贴到存储过程。

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

如果遇到错误，可能需要对查询文本进行一些编辑。 例如，必须用两组单引号将 WHERE 子句中的字符串谓词括起来。

正常运行查询后，请查看 `str` 函数的结果，了解 R 如何处理输入数据。

**结果**

```sql
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

- 日期时间列已使用 R 数据类型 **POSIXct** 进行处理。
- 文本列 "ProductSeries" 已被标识为一个**系数**, 即分类变量。 默认情况下，字符串值将作为因子处理。 如果将某个字符串传递给 R，该字符串将转换为整数供内部使用，然后映射回到输出中的字符串。

### <a name="summary"></a>总结

从甚至这些简短的示例中, 您可以看到在将 SQL 查询作为输入进行传递时, 需要检查数据转换的影响。 由于 R 不支持某些 SQL Server 数据类型, 因此请考虑使用以下方法来避免错误:

- 提前测试数据, 并验证架构中的列或值在传递到 R 代码时可能会出现问题。
- 在输入数据源中单独指定列而不要使用 `SELECT *`，并知道如何处理每个列。
- 准备输入数据时请根据需要执行显式强制转换，避免出现意外。
- 避免传递导致错误的数据列 (例如 GUID 或 rowguid), 这对建模不起作用。

有关支持的和不支持的数据类型的详细信息, 请参阅[R 库和数据类型](../r/r-libraries-and-data-types.md)。

有关对字符串的运行时转换到数值因素的性能影响的信息, 请参阅[SQL Server R Services 性能优化](../r/sql-server-r-services-performance-tuning.md)。

## <a name="next-steps"></a>后续步骤

若要了解如何在 SQL Server 中编写高级 R 函数，请按照本快速入门：

> [!div class="nextstepaction"]
> [通过 SQL Server 机器学习服务写入高级 R 函数](quickstart-r-functions.md)

有关 SQL Server 机器学习服务的详细信息，请参阅：

- [什么是 SQL Server 机器学习服务（Python 和 R）？](../what-is-sql-server-machine-learning.md)
