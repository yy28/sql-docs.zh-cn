---
title: sp_execute_external_script (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/14/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 4421ac28e3ee8914cf016f5df23e5f163bacfd9b
ms.sourcegitcommit: a251adad8474b477363df6a121431b837f22bf77
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47864395"
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script (TRANSACT-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

执行作为该过程的输入参数提供的脚本。 在运行脚本[可扩展性框架](../../advanced-analytics/concepts/extensibility-framework.md)。 必须具有至少一个扩展的数据库引擎上支持并已注册的语言、 编写脚本： [ **R**](../../advanced-analytics/concepts/extension-r.md)， [ **Python** ](../../advanced-analytics/concepts/extension-python.md)或[ **Java** （在 SQL Server 2019 限预览版本）](../../advanced-analytics/java/extension-java.md)。 

若要执行**sp_execute_external_script**，必须先通过使用该语句中，启用外部脚本`sp_configure 'external scripts enabled', 1;`。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

> [!Note]
> 机器学习 （R 和 Python） 和编程扩展会安装到数据库引擎实例的外接程序。 对特定扩展的支持因 SQL Server 版本而异。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax"></a>语法

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]    
    [ , @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end
::: moniker range=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"
## <a name="syntax-for-2017-and-earlier"></a>语法 2017 及更早版本

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end

## <a name="arguments"></a>参数
 **@language** = N'*语言*  
 指示脚本语言。 *语言*是**sysname**。  具体取决于你的 SQL Server 版本，有效的值为 R (SQL Server 2016 及更高版本)、 Python (SQL Server 2017 及更高版本) 和 Java （SQL Server 2019 预览版）。 
  
 **@script** = N'*脚本*指定为参数或变量的输入的外部语言脚本。 *脚本*是**nvarchar （max)**。  

  [ **@input_data_1** = N'*input_data_1*']  
 指定使用的窗体中的外部脚本的输入的数据[!INCLUDE[tsql](../../includes/tsql-md.md)]查询。 数据类型*input_data_1*是**nvarchar （max)**。

 [ **@input_data_1_name** = N'*input_data_1_name*']  
 指定用于表示定义的查询变量的名称@input_data_1。 外部脚本的变量中的数据类型取决于语言。 对于 R，则输入的变量是数据帧。 对于 Python，输入必须为表格。 *input_data_1_name*是**sysname**。  默认值是*InputDataSet*。  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
  [ **@input_data_1_order_by_columns** = N'*input_data_1_order_by_columns*']  
 仅适用于 SQL Server 2019，用于生成每个分区模型。 指定的列用于排序的结果集，例如按产品名称的名称。 外部脚本的变量中的数据类型取决于语言。 对于 R，则输入的变量是数据帧。 对于 Python，输入必须为表格。

  [ **@input_data_1_partition_by_columns** = N'*input_data_1_partition_by_columns*']  
 仅适用于 SQL Server 2019，用于生成每个分区模型。 指定用于对段数据，例如，地理区域或日期的列的名称。 外部脚本的变量中的数据类型取决于语言。 对于 R，则输入的变量是数据帧。 对于 Python，输入必须为表格。 
::: moniker-end

 [ **@output_data_1_name** = N'*output_data_1_name*']  
 指定的变量名称中包含要返回到的数据的外部脚本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]存储的过程调用完成后。 外部脚本的变量中的数据类型取决于语言。 对于 R，输出必须是数据帧。 对于 Python，输出必须为 pandas 数据帧。 *output_data_1_name*是**sysname**。  默认值是*OutputDataSet*。  

 [ **@parallel** = 0 | 1]  
 通过设置启用并行执行 R 脚本`@parallel`参数为 1。 为此参数默认值为 0 （不能并行）。 如果`@parallel = 1`和输出进行流式处理直接向客户端计算机，则`WITH RESULT SETS`子句是必需的并且必须指定输出架构。  

 + 为不使用 RevoScaleR 函数，请使用 R 脚本`@parallel`参数可以是有益于处理大型数据集，假设可以不费力地并行执行该脚本。 例如，在使用 R`predict`函数和一个模型来生成新预测，设置`@parallel = 1`作为对查询引擎的提示。 如果可以并行执行查询，将行分布根据**MAXDOP**设置。  
  
 + 使用 RevoScaleR 函数的 R 脚本，并行处理进行处理自动，并且不应指定`@parallel = 1`到**sp_execute_external_script**调用。  
  
[ **@params** = N' *@parameter_name data_type* [出 |输出] [，....n]']  
 外部脚本中使用的输入的参数声明的列表。  
  
[ **@parameter1** = '*value1*[出 |输出] [，....n]]  
 有关使用外部脚本的输入参数的值的列表。  

## <a name="remarks"></a>备注

> [!IMPORTANT]
> 由控制查询树[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，用户无法执行该查询的任意操作。 

使用**sp_execute_external_script**执行以受支持的语言编写的脚本。 目前，支持的语言是 SQL Server 2016 R Services，和 Python 和 R 的 SQL Server 2017 机器学习服务的 R。 

默认情况下，此存储过程返回的结果集是使用未命名的列的输出。 列名称的脚本中使用脚本编写环境和本地不会反映在输出的结果集。 若要命名结果集列，使用`WITH RESULT SET`子句[ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md)。
  
 除了返回的结果集，可以返回标量值到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用输出参数。 下面的示例显示了输出参数可返回已用作输入的脚本的序列化的 R 模型的使用：  
  
您可以控制通过配置的外部资源池使用外部脚本的资源。 有关详细信息，请参阅 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。 可以从资源调控器目录视图、 DMV 和计数器获取工作负荷的相关信息。 有关详细信息，请参阅[资源调控器目录视图&#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)，[资源调控器相关的动态管理视图&#40;-&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)，和[SQL Server-External Scripts 对象](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)。  

### <a name="monitor-script-execution"></a>监视脚本执行

监视脚本执行使用[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)并[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)。 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>参数用于分区建模

 在 SQL Server 2019 目前处于公共预览状态，可以设置两个其他参数，使对已分区数据，其中分区都基于一个或更多的列提供的自然地细分为逻辑分区的数据集创建和使用的建模仅在脚本执行。 年龄、 性别、 地理区域、 日期或时间，对于包含重复值的列是几个示例都适用于已分区的数据集。
 
 两个参数是**input_data_1_partition_by_columns**并**input_data_1_order_by_columns**，第二个参数用于结果集进行排序。 作为输入传递的参数`sp_execute_external_script`与外部脚本执行一次每个分区。 有关详细信息和示例，请参阅[教程： 创建基于分区的模型](https://docs.microsoft.com/sql/advanced-analytics/tutorials/r-tutorial-create-models-per-partition.md)。

 可以通过指定并行执行脚本`@parallel=1`。 如果输入的查询可并行化，则应设置`@parallel=1`作为你的参数的一部分`sp_execute_external_script`。 默认情况下，查询优化器将在操作`@parallel=1`对表具有 256 个以上的行，但如果你想要显式处理这种情况，此脚本包括作为演示参数。

 > [!Tip]
> 对于训练 workoads，可以使用`@parallel`任何任意训练脚本，甚至包括那些使用非 Microsoft rx 算法。 通常情况下，仅 RevoScaleR 算法 （与 rx 前缀） 产品/服务中 SQL Server 中的培训方案的并行度。 但使用 SQL Server vNext 中新的参数，您可以并行化调用函数不是专门设计，提供该功能的脚本。
::: moniker-end

### <a name="streaming-execution-for-r-and-python-scripts"></a>流式处理执行的 R 和 Python 脚本  

使用流式技术，用于处理更多的数据多于可以容纳在内存中的 R 或 Python 脚本。 若要控制流式处理过程中传递的行数，请指定参数，一个整数值`@r_rowsPerRead`在`@params`集合。  例如，如果将训练一个使用非常宽的数据模型，您可以调整要读取更少的行，以确保可以在一个数据块区发送所有行的值。 您可能会使用此参数来管理正在读取和处理一次来缓解服务器性能问题的行数。 
  
这两个`@r_rowsPerRead`流式处理的参数和`@parallel`参数应被认为的提示。 要应用的提示，它必须能生成包含并行处理的 SQL 查询计划。 如果这不是可能的不能启用并行处理。  
  
> [!NOTE]  
>  仅在 Enterprise Edition 中支持流式处理和并行处理。 你可以在标准版在查询中包含参数，并且不会引发错误，但参数具有任何作用，而且在单个进程中运行 R 脚本。  
  
## <a name="restrictions"></a>限制  


### <a name="data-types"></a>数据类型

输入的查询或参数中使用时不支持以下数据类型**sp_execute_external_script**过程中，并返回类型不受支持的错误。  

解决方法是， **CAST**中的受支持类型的值的列[!INCLUDE[tsql](../../includes/tsql-md.md)]之前将其发送到外部脚本。  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**， **datetimeoffset**，**时间**  
  
-   **sql_variant**  
  
-   **文本**，**图像**  
  
-   **xml**  
  
-   **hierarchyid**， **geometry**， **geography**  
  
-   CLR 用户定义的类型

一般情况下，任何结果集不能映射到[!INCLUDE[tsql](../../includes/tsql-md.md)]数据类型，则输出为 NULL。  

### <a name="restrictions-specific-to-r"></a>特定于 R 的限制

如果输入包含**datetime**不适合在 R 中的值的允许范围的值，将值转换为**NA**。 这是必需的因为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]允许更大的值不是 R 语言中支持范围。

浮点值 (例如， `+Inf`， `-Inf`， `NaN`) 中不支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]即使这两种语言使用 IEEE 754。 当前行为只是在发送到的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]直接; 因此中的 SQL 客户端[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]将引发错误。 因此，将这些值转换为**NULL**。

## <a name="permissions"></a>Permissions

需要**EXECUTE ANY EXTERNAL SCRIPT**数据库权限。  

## <a name="examples"></a>示例

本部分包含如何使用此存储的过程来执行使用的 R 或 Python 脚本的示例[!INCLUDE[tsql](../../includes/tsql-md.md)]。

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. 返回到 SQL Server 的 R 数据集  

下面的示例创建使用的存储的过程**sp_execute_external_script**返回到 R 中包含的鸢尾花数据集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  

```sql
DROP PROC IF EXISTS get_iris_dataset;  
go  
CREATE PROC get_iris_dataset
AS  
BEGIN  
 EXEC   sp_execute_external_script  
       @language = N'R'  
     , @script = N'iris_data <- iris;'
     , @input_data_1 = N''  
     , @output_data_1_name = N'iris_data'
     WITH RESULT SETS (("Sepal.Length" float not null,   
           "Sepal.Width" float not null,  
        "Petal.Length" float not null,   
        "Petal.Width" float not null, "Species" varchar(100)));  
END;
GO
```

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. 生成基于数据从 SQL Server 的 R 模型  

下面的示例创建使用的存储的过程**sp_execute_external_script**生成鸢尾花模型并返回到模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  

> [!NOTE]
>  此示例需要提前 e1071 包安装。 有关详细信息，请参阅[SQL Server 上安装其他 R 包](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)。

```sql
DROP PROC IF EXISTS generate_iris_model;
GO
CREATE PROC generate_iris_model
AS
BEGIN
 EXEC sp_execute_external_script  
      @language = N'R'  
     , @script = N'  
          library(e1071);  
          irismodel <-naiveBayes(iris_data[,1:4], iris_data[,5]);  
          trained_model <- data.frame(payload = as.raw(serialize(irismodel, connection=NULL)));  
'  
     , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from iris_data'  
     , @input_data_1_name = N'iris_data'  
     , @output_data_1_name = N'trained_model'  
    WITH RESULT SETS ((model varbinary(max)));  
END;
GO
```

要生成使用 Python 的类似模型，需要将语言标识符从 `@language=N'R'` 更改为 `@language = N'Python'`，并对 `@script` 参数进行必要的修改。 否则，所有参数均与 R 在功能上相同。

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. 创建 Python 模型并从中生成分数

本示例演示了如何使用 sp\_execute\_external\_ 在 Python 模型中生成分数。 

```sql
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

-- Input query to generate the customer data
DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders'

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

# Get data from input query
customer_data = my_input_data

# Define the model
n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

使用 Python 代码中的列标题不是输出到 SQL Server;因此，使用与结果语句指定的列名称和 SQL 使用的数据类型。

要进行评分，还可以使用本机 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 函数，此函数无需调用 Python 或 R 运行时，因此更加快速。

## <a name="see-also"></a>另请参阅

 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Python 库和数据类型](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [R 库和 R 数据类型](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)   
 [SQL Server 机器学习服务的已知的问题](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
 [创建外部库&#40;Transact SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [external scripts enabled 服务器配置选项](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)   
 [SQL Server - External Scripts 对象](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
