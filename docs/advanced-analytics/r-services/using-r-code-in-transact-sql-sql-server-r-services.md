---
title: "在 Transact-SQL 中使用 R 代码 (SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: 36
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 28
---
# 在 Transact-SQL 中使用 R 代码 (SQL Server R Services)
本教程提供了在 SQL Server R 服务中使用 R 的语法的简短示例。    
    
    
请先参阅这些示例来熟悉 SQL Server R 服务，并基本了解如何在 T-SQL 存储过程中定义 R 脚本、如何将数据用作输入，以及如何定义输出。    
    
**先决条件：**若要在 SQL Server R 服务中运行 R 代码，必须连接到安装了 R 服务的 SQL Server 的实例。     
    
## 第 1 部分 - 基本操作  

在以下部分中，将了解如何通过添加参数扩展存储过程以及如何配置输入和输出。   
  
### 1.1. 检查 R 是否在 SQL Server 中运行  

此查询使用系统存储过程 [sp_execute_external_script](https://msdn.microsoft.com/library/mt604368.aspx)，这是在 SQL Server 的上下文中调用 R 的方式。 此示例将 SQL 查询作为输入传递到 R，而 R 将该数据帧返回到 SQL Server。     
    
1. 在 Windows“开始”菜单中，找到 Microsoft SQL Server Management Studio。     
2. 如果未找到，可能需要进行安装：[下载 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。    
3. 在“连接到服务器”对话框中，键入启用了 SQL Server R 服务的服务器/实例的名称。 对于这些示例，请确保使用具有以下功能的帐户进行登录：创建新数据库、运行 SELECT 语句，及查看表。  打开一个新的“查询”窗口，并粘贴此语句，检查一切是否正常：    
    
    ```sql   
    exec sp_execute_external_script  
      @language =N'R',    
      @script=N'OutputDataSet<-InputDataSet',      
      @input_data_1 =N'select 1 as hello'    
      with result sets (([hello] int not null));    
    go    
    ```   
       
       
  
### <a name="bkmk_SSMSBasics"></a>1.2. 创建一些简单的测试数据  
    
开发复杂的数据科学解决方案之前，了解 SQL Server 和 R 之间的差异很重要。    
  
1. 运行以下 T-SQL 语句来创建临时数据表。     
   
    ```sql    
    CREATE TABLE #MyData ([Col1] int not null) ON [PRIMARY]    
    INSERT INTO #MyData   VALUES (1);    
    INSERT INTO #MyData   Values (10);    
    INSERT INTO #MyData   Values (100) ;    
    GO    
    ```    
5. 成功创建表后，使用以下语句对表进行查询：  
    ```sql  
    SELECT * from #MyData  
    ```  

**结果**  
  
|Col1 |   
|----|   
|1|   
|10|   
|100|   
  
    
### 1.3. 使用 R 脚本获取测试数据    
  
成功创建表后，运行以下语句：  
  
  ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet <- InputDataSet;'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
    WITH RESULT SETS (([NewColName] int NOT NULL));
  ```    
    
应返回相同的值，但具有新的列名称。  
  
**说明**    
- @Language 参数定义本例中要调用 R 的语言扩展。    
- 在 @script 参数中，定义命令以 Unicode 文本传递到 R 运行时。 还可将文本添加到 **nvarchar** 类型的变量并调用该变量。    
- `N'OutputDataSet <- InputDataSet;'` 行会将默认变量名称 **InputDataSet** 中所含的输入数据传递到 R，然后返回到结果，无需再执行任何操作。 请注意，R 会区分大小写；因此，输入变量名称和输出变量名称必须使用正确的大小写，否则将产生错误。    
   
    
若要指定不同的输入变量或输出变量，请使用 @input_data_1_name 参数并键入有效的 SQL 标识符。 例如，在此示例中，输出变量和输入变量的名称已分别变为 *SQLOut* 和 *SQLIn*：    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' SQLOut <- SQLIn;'    
    , @input_data_1 = N' SELECT 12 as Col;'    
    , @input_data_1_name  = N'SQLIn'    
    , @output_data_1_name =  N'SQLOut'    
    WITH RESULT SETS (([NewColName] int NOT NULL));    
```    
    
**说明**    
- 必须首先指定必需的参数 @input_data_1 和 @output_data_1，以使用可选参数 @input_data_1_name 和 @output_data_1_name。    
- SQL 和 R 不支持相同的数据类型；因此，从 SQL Server 发送数据到 R 时，类型转换非常频繁，反之亦然。 有关详细信息，请参阅[使用 R 数据类型](../../advanced-analytics/r-services/working-with-r-data-types.md)。    
- 仅可将一个输入数据集作为参数传递，且仅可返回一个数据集。 但是，可以从 R 代码内调用其他数据集，并且除数据集以外，还可以返回其他类型的输出。 还可以向任何参数添加 OUTPUT 关键字，使其随结果一起返回。      
- 返回数据集的架构 (R data.frame) 由 `WITH RESULT SETS` 语句定义。 尝试省略此语句，看看会出现什么情况。    
- 表格结果返回在“值”窗格中。 R 运行时返回的消息在“消息”中提供     
  
### 1.4. 使用 R 生成结果    
    
还可仅使用 R 脚本来生成值，并将 _@input_data_1_ 中的输入查询字符串留空。 或者，可使用有效的 SQL SELECT 语句作为占位符，但不要在 R 脚本中使用 SQL 结果。    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' mytextvariable <- c("hello", " ", "world");    
                         OutputDataSet <- as.data.frame(mytextvariable);'    
    , @input_data_1 = N' SELECT 1 as Temp1'    
    WITH RESULT SETS (([col] char(20) NOT NULL));    
```    
    
**结果**    
    
    
 |*col* |    
 |-----|    
 |*Hello*|    
 |     |    
 |*world*|    
    

现在，请尝试与上述 Hello World 示例不同的版本。     
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'    
    , @input_data_1 = N'  '    
    WITH RESULT SETS (([col1] varchar(20) , [col2] char(1), [col3] varchar(20) ));    
```    
    
    
**结果**    
    
    
 |*col1* | *col2* | *col3*|    
 |-------|-------|-------    
 |*Hello*|  |*world*|    
    
请注意，这两个语句都会创建一个具有 3 个值的向量，但第二个示例返回 3 列和单行，而第一个示例返回 3 行和单列。 原因是什么？
    
这是因为 R 提供多种方式来处理多列值：向量、矩阵、数组和列表。 尽管这些操作功能强大且灵活，但也不总能达到 SQL 开发人员的期望。  某些 R 函数在列表和矩阵上执行隐式数据对象转换。

> [!TIP] 
> 
> 始终验证结果，确定 R 代码将返回多少列数据及其数据类型。    
>     
> 无论 R 代码使用矩阵、向量还是某些其他数据结构，都请记住：从 R 脚本输出到存储过程的结果到必须为 **data.frame**。      
  
  
## 第 2 部分 - 数据转换及其他问题  
  
本部分简要概述了在 SQL Server 中运行 R 代码时应注意的某些问题。  
  
+ 数据类型：了解强制转换、转换选项和隐式转换  
+ 表格结果集：预测 R 可更改数据行和列的方法    
  
### 2.1 数据类型的隐式强制转换  
    
R 和 SQL Server 使用不同的数据类型，因此在 R 和数据库之间移动数据时，需注意相关限制。 以下示例说明了一些常见问题。   
    
    
1. 使用 R 运行以下语句来执行矩阵乘法操作。在此脚本中，带 3 个值的单列被转换为单列矩阵。  然后，R 将第二个变量 `y` 隐式强制转换为单列矩阵，使两个参数符合。  
    
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:15);    
      OutputDataSet <- as.data.frame(x %*% y);'    
     , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));    
    ```    
**结果**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|
 
  
      
2. 现在运行下一个相似脚本，观察更改数组长度后会出现什么情况。 
   
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:14);    
      OutputDataSet <- as.data.frame(y %*% x);'    
      , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int ));    
    ```    

**结果**    
    
|Col1|
|---|    
|1542|    
  
  R 这次返回单个值作为结果。 此结果有效，因为这两个参数是长度相同的向量；因此，R 将以矩阵形式返回内部产品。    
    
   
  
### 2.2 对不同长度的列进行合并或拆分    
    
  
以下脚本说明 R 的某些行为可能不符合数据库开发人员的期望。   
  
该脚本定义了长度为 6 的新数值数组，并将其存储在 R 变量 `df1` 中。 然后将该数值数组与包含 3 个值的 #MyData 表的整数组合，形成新的数据帧 `df2`。   
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
               df1 <- as.data.frame( array(1:6) );    
               df2 <- as.data.frame( c( InputDataSet , df1 ));    
               OutputDataSet <- df2'    
    , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));    
```    
    
**结果**    
    
|*Col2*|*Col3*|    
|----|----|    
|1|1|    
|10|2|    
|100|3|    
|1|4|    
|10|5|    
|100|6|    
    
R 中有许多函数可创建表格输出，但根据 R 数据对象，对值执行的操作却大不相同。 因为此 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程需要将输入和输出作为 data.frame 传递，所以将很频繁地使用函数在列与行和数据帧之间来回转换。    
    
如果不确定正在使用哪种 R 数据对象，请添加 R `str()` 函数或标识函数（`is.matrix`、`is.vector`等）之一来检查结果并获取实际架构和值类型。    
  
  
有关详细信息，请参阅 Hadley Wickham 撰写的文章 [R 数据结构](http://adv-r.had.co.nz/Data-structures.html)。    
    
### 2.3 标识数据类型并验证架构   
可见确定 R 代码将返回多少列数据以及每列的数据类型的重要性。     
    
  
可以在 R 脚本中使用函数 `str()`，使 R 对象的数据架构作为信息性消息返回。 

例如，以下语句返回 #MyData 表的架构。    
        
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' str(InputDataSet);'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
      WITH RESULT SETS undefined;    
```    
    
    
**结果**    
    
*STDOUT message (s) from external script:*    
*'data.frame': 3 obs. of 1 variable:*    
*STDOUT message (s) from external script:*    
*$ Col1: int 1   10   100*    
    
  
  
### 2.4 强制转换或转换列   
  
将数据从 SQL Server 发送到 R 时，经常需要强制转换或转换数据类型，以确保可对其进行适当的处理。    
  
将 SQL 查询用作 R 代码的输入时，会发生多个数据转换：    
- SQL Server 将数据从查询推送到由启动板服务管理的 R 进程，并将其转换为内部表示形式。    
- R 运行时将数据加载到 data.frame 变量中，并对数据执行其自身的操作。    
- 数据库引擎将数据返回到 Management Studio 或使用 SQL Server 数据类型的另一个客户端。  
    
1. 在 AdventureWorksDW 数据仓库上运行以下查询。 输入数据查询定义用于创建预测的销售数据表。   
  
    ```sql    
    execute sp_execute_external_script    
       @language = N'R'    
      , @script = N' str(InputDataSet);'    
      , @input_data_1 = N'
           SELECT ReportingDate    
         , CAST(ModelRegion as varchar(50)) as ProductSeries    
         , Amount    
           FROM [AdventureworksDW2016CTP3].[dbo].[vTimeSeries]     
           WHERE [ModelRegion] = ''M200 Europe''    
           ORDER BY ReportingDate ASC ;'    
        WITH RESULT SETS undefined;    
    ```    
  
2. 现请查看 `str` 函数的结果，查看 R 如何处理输入数据。
      
**结果**    
    
  *STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:*    
  *STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"*    
  *STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1 ...*    
  *STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950*    
    
    
**说明**    
    
- R 不支持某些 SQL Server 数据类型。因此，为避免发生错误，应单独指定列并强制转换某些列。    
- 必须用两组单引号将 WHERE 子句中的字符串谓词括起来。    
- 已以 R 数据类型 **POSIXct**返回 datetime 列。    
- 已将 [ProductSeries] 列（正确）识别为**因素**。    
     
  
### 2.5 使用多个输入   
仅可将一个输入数据集作为参数传递。 但是，可以使用 RODBC 从 R 代码内调用其他数据集。     
  
例如，以下示例调用了 RODBC 包，在 SELECT 语句中指定了数据。    
    
```sql    
    @script = N' 
       <other R code here>;    
       library(RODBC);    
       connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");        dbhandle <- odbcDriverConnect(connStr)    
       OutputDataSet <- sqlQuery(dbhandle, "SELECT * from <table_name>");    
       <more R code combining the data>'    
```

建议通过 SQL Server 使用 RODBC 获取较小的数据集，例如查找次数或因素列表，并使用 @input_data 参数获取大型数据集，例如用于定型模型的数据集。 


### 2.6 生成多个输出

在 SQL Server 2016 中，存储过程 sp_execute_external_script 的 R 输出仅限于单个 data.frame 或数据集。 （将来可能会去除此限制。）   
但是，除数据集以外，还可以返回其他类型的输出。 例如，可以将使用单个数据集的模型定型为输入，而返回的统计信息表作为输出，以及已定型的模型作为对象。    
    
此外，可以向任何输入参数添加 `OUTPUT` 关键字，使其返随结果一起返回。   
    
### 2.7 并行处理    
    
如果正在处理大型数据集，且获取数据的 SQL 查询可以生成并行查询计划，则可以通过将 *@parallel* 参数设置为 1 并行运行 R 脚本。 对大型结果集进行评分时，这通常很有用。 如果使用此选项，则必须事先使用 WITH RESULT SETS 指定输出结果架构。    
    
但是，如果需要定型使用所有行的模型，此参数不会产生任何影响；对于这种情况，我们建议使用 **ScaleR** 包。 这些包可以自动进行分布式处理，无需在对 sp_execute_external_script 的调用中指定 *@parallel =1*。    
    
      
  
## 第 3 部分. 在存储过程中包装 R 函数  
  
R 可执行很多高级统计函数，这些函数可能需要复杂的代码以使用 T-SQL 进行重现。  但是，R 服务可在存储过程中运行 R 实用工具脚本，以支持此类任务：   
    
- 将 R 的数学和统计函数应用到 SQL Server 数据    
    
- 创建表值函数或使用 R 代码的标量函数    
     

 通常情况下，将对这些 R 函数的调用封装在存储过程中，以便其更容易在参数中传递。 为了说明此过程，在 R 代码中、对 sp_execute_external_script 的临时存储过程调用中，以及在可用于参数化 R 函数的存储过程中使用相同的函数。
 
      
### 3.1. 生成随机数字  
  
以下语句使用的 `stats` 包中的某个 R 函数，该包在安装 R Services 时默认加载。 此处显示的 `rnorm` 函数生成 20 个随机数字，这些数字呈正态分布，且给定的平均值为 100。    

以下 R 代码用于执行工作。

```r
as.data.frame(rnorm(20, mean = 100));
```

此语句从 T-SQL 调用函数，并将结果输出到 SQL Server。  
   
```sql    
EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N' 
         OutputDataSet <- as.data.frame(rnorm(20, mean = 100));'    
    , @input_data_1 = N'   ;'    
      WITH RESULT SETS (([Density] float NOT NULL));    
```    

接下来，将存储过程打包到另一个存储过程中，以便更容易在参数中传递。 必须定义 _@params_ 参数中的每个输入参数，并按名称将每个参数映射到对应的 R 参数。

```sql
CREATE PROCEDURE MyRNorm (@mynorm int, @mymean int)
AS
    EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynorm, mymean));'    
    , @input_data_1 = N'   ;' 
    , @params = N' @mynorm int, @mymean int'  
    , @mynorm = @mynorm
    , @mymean = @mymean
    WITH RESULT SETS (([Density] float NOT NULL));    
```

调用新的存储过程，并以值传递。

```sql
exec MyRNorm @mynorm = 20,@mymean = 100
```  
    
### 3.2 R 实用工具函数的更多功能  
  
此示例调用了一个 R 实用包，并使用其 `memory.limit()` 函数获取当前环境的内存。 安装有 `utils` 包，但未默认加载。    
    
```sql    
execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
        library(utils);    
        mymemory <- memory.limit();    
        OutputDataSet <- as.data.frame(mymemory);'    
    , @input_data_1 = N' ;'    
     WITH RESULT SETS (([Col1] int not null));    
```    

以下示例利用 R .Machine 函数获取当前计算机支持的最大整数长度，并将其输出到控制台。

```R
localmax <- .Machine$integer.max;
localmax;
```

```sql
execute sp_execute_external_script
  @language = N'R'
  , @script = N'
      localmax <- .Machine$integer.max;
      OutputDataSet <- as.data.frame(localmax);'
  , @input_data_1 = N'select [Col1]  from #MyData;'
  WITH RESULT SETS (([MaxIntValue] int not null));
```     
    
但是，R 也并非总是如此出色地完成工作。 对于数据科学家习惯在 R 中执行的某些操作而言，SQL Server 中基于集的操作可能更加高效。有关 R 函数和 T-SQL 自定义函数性能比较的示例，请参阅 [数据科学端到端解决方案](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)。 

建议根据具体情况评估是否使用 R、T-SQL 或是其他一些工具执行给定的操作会更有意义。    
    
    
    
### 其他资源    
    
[对数据科学的深入探讨：使用 RevoScaleR 包](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)：本演练提供了常用数据科学任务的亲身体验    
[数据科学端到端解决方案](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)：本演练介绍了平衡 SQL 和 R 方法的开发和部署过程       
[ SQL 开发人员的高级分析](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)：介绍了完整模型操作化 SQL 开发人员     
    
    
    
    
