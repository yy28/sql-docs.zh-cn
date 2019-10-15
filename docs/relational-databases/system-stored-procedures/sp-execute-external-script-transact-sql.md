---
title: sp_execute_external_script （Transact-sql） |Microsoft Docs
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
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 6a7eb58883a94f1eb29d2c7e26e52768f4e08d9e
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304935"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

执行以输入参数形式提供给过程的脚本。 可在[扩展性框架](../../advanced-analytics/concepts/extensibility-framework.md)中运行脚本。 对于至少具有一个扩展名的数据库引擎，必须使用支持的注册语言编写脚本：[**R**](../../advanced-analytics/concepts/extension-r.md)、 [**Python**](../../advanced-analytics/concepts/extension-python.md)或[ **Java** （仅限 SQL Server 2019 预览版）](../../advanced-analytics/java/extension-java.md)。 

若要执行**sp_execute_external_script**，必须先通过使用语句 `sp_configure 'external scripts enabled', 1;` 来启用外部脚本。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

> [!Note]
> 机器学习（R 和 Python）和编程扩展作为外接程序安装到数据库引擎实例中。 SQL Server 版本不同，对特定扩展的支持有所不同。

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
## <a name="syntax-for-2017-and-earlier"></a>2017及更早版本的语法

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
 **\@language** = N "*language*"  
 指示脚本语言。 *语言*为**sysname**。  根据您的 SQL Server 版本，有效值为 R （SQL Server 2016 及更高版本）、Python （SQL Server 2017 及更高版本）和 Java （SQL Server 2019 预览版）。 
  
 **\@script** = N "*script*" 外部语言脚本指定为文本或变量输入。 *脚本*为**nvarchar （max）** 。  

`[ @input_data_1 =  N'input_data_1' ]` 指定外部脚本使用的输入数据，格式为 @no__t 查询。 *Input_data_1*的数据类型为**nvarchar （max）** 。

@no__t 指定用于表示 @input_data_1 定义的查询的变量名称。 外部脚本中的变量的数据类型取决于语言。 对于 R，输入变量是数据帧。 对于 Python，输入必须为表格格式。 *input_data_1_name*为**sysname**。  默认值为*InputDataSet*。  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]` 仅适用于 SQL Server 2019，用于构建每个分区模型。 指定用于对结果集进行排序的列的名称，例如 "产品名称"。 外部脚本中的变量的数据类型取决于语言。 对于 R，输入变量是数据帧。 对于 Python，输入必须为表格格式。

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]` 仅适用于 SQL Server 2019，用于构建每个分区模型。 指定用于对数据进行分段的列的名称，如地理区域或日期。 外部脚本中的变量的数据类型取决于语言。 对于 R，输入变量是数据帧。 对于 Python，输入必须为表格格式。 
::: moniker-end

@no__t 指定包含要在完成存储过程调用时返回到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的数据的外部脚本中的变量的名称。 外部脚本中的变量的数据类型取决于语言。 对于 R，输出必须是数据帧。 对于 Python，输出必须为 pandas 数据帧。 *output_data_1_name*为**sysname**。  默认值为*OutputDataSet*。  

`[ @parallel = 0 | 1 ]` 通过将 @no__t 参数设置为1来启用 R 脚本的并行执行。 此参数的默认值为0（无并行）。 如果 `@parallel = 1`，并且输出将直接流式传输到客户端计算机，则必须指定 `WITH RESULT SETS` 子句并指定输出架构。  

 + 对于不使用 RevoScaleR 函数的 R 脚本，使用 `@parallel` 参数对于处理大型数据集非常有利，假设脚本可以完全并行化。 例如，使用带有模型的 R `predict` 函数生成新的预测时，请将 @no__t 为提示设置为查询引擎。 如果可以并行化查询，行将按照**MAXDOP**设置进行分布。  
  
 + 对于使用 RevoScaleR 函数的 R 脚本，会自动处理并行处理，不应将 @no__t 0 指定给**sp_execute_external_script**调用。  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]` 在外部脚本中使用的输入参数声明的列表。  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]` 外部脚本使用的输入参数的值列表。  

## <a name="remarks"></a>备注

> [!IMPORTANT]
> 查询树由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 控制，并且用户无法对查询执行任意操作。 

使用**sp_execute_external_script**可以执行以支持的语言编写的脚本。 目前，支持的语言是 R，适用于 SQL Server 2016 R 服务，以及用于 SQL Server 2017 机器学习服务的 Python 和 R。 

默认情况下，此存储过程返回的结果集是具有未命名列的输出。 脚本中使用的列名是脚本环境的本地列名，不会反映在输出结果集中。 若要命名结果集列，请使用[@no__t](../../t-sql/language-elements/execute-transact-sql.md)的 @no__t 子句。
  
 除了返回一个结果集外，还可以使用 OUTPUT 参数将标量值返回到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 下面的示例演示如何使用 OUTPUT 参数返回用作脚本输入的序列化 R 模型：  
  
可以通过配置外部资源池来控制外部脚本所使用的资源。 有关详细信息，请参阅 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。 可从资源调控器目录视图、DMV 和计数器获取有关工作负荷的信息。 有关详细信息，请参阅[Resource Governor Catalog &#40;Views&#41;transact-sql](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)、 [Resource Governor 相关的动态管理视图&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)和[SQL Server 外部脚本对象](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)。  

### <a name="monitor-script-execution"></a>监视脚本执行

使用[sys.databases _external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)和[sys.databases _external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)监视脚本执行。 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>分区建模的参数

 在 SQL Server 2019 （目前为公共预览版）中，可以设置两个附加参数，这些参数对分区数据启用建模，其中分区基于你提供的一个或多个列，这些列将数据集自然分段为创建和使用的逻辑分区仅在脚本执行期间。 包含年龄、性别、地理区域、日期或时间的重复值的列是几个可用于分区数据集的示例。
 
 这两个参数是**input_data_1_partition_by_columns**和**input_data_1_order_by_columns**，其中第二个参数用于对结果集进行排序。 参数作为输入传递到 `sp_execute_external_script`，并为每个分区执行一次外部脚本。 有关详细信息和示例，请参阅 [Tutorial：创建基于分区的模型 @ no__t。

 可以通过指定 `@parallel=1` 并行执行脚本。 如果输入查询可并行化，则应将 `@parallel=1` 设置为 @no__t 的参数的一部分。 默认情况下，查询优化器将在256行以上的表中 `@parallel=1` 运行，但如果要显式处理此操作，则此脚本将参数作为演示。

 > [!Tip]
> 对于定型 workoads，可以将 `@parallel` 与任何任意定型脚本（甚至使用非 Microsoft rx 算法的脚本）一起使用。 通常，只有 RevoScaleR 算法（带有 rx 前缀）在 SQL Server 的定型方案中提供并行度。 但使用 SQL Server vNext 中的新参数，可以并行化脚本，该脚本调用未使用该功能专门设计的函数。
::: moniker-end

### <a name="streaming-execution-for-r-and-python-scripts"></a>R 和 Python 脚本的流式执行  

流式处理允许 R 或 Python 脚本处理的数据量超过内存中可以容纳的数据量。 若要控制在流式处理期间传递的行数，请为参数指定一个整数值，@no__t 在 @no__t 集合中为0。  例如，如果您在定型使用非常宽数据的模型，则可以调整该值以读取较少的行，以确保所有行都可以在一个数据块中发送。 你还可以使用此参数来管理一次读取和处理的行数，以减少服务器性能问题。 
  
用于流式处理的 @no__t 0 参数和 @no__t 参数都应视为提示。 若要应用提示，必须能够生成包含并行处理的 SQL 查询计划。 如果这是不可能的，则不能启用并行处理。  
  
> [!NOTE]  
>  只有 Enterprise Edition 支持流式处理和并行处理。 你可以在标准版的查询中包含参数，而不会引发错误，但参数不起作用，并且 R 脚本在单个进程中运行。  
  
## <a name="restrictions"></a>限制  


### <a name="data-types"></a>数据类型

如果在**sp_execute_external_script**过程的输入查询或参数中使用了以下数据类型，并返回了不受支持的类型错误。  

解决方法是将列或值**转换**为 @no__t 中的受支持的类型，然后再将其发送到外部脚本。  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**、 **datetimeoffset**、 **time**  
  
-   **sql_variant**  
  
-   **文本**、**图像**  
  
-   **xml**  
  
-   **hierarchyid**、 **geometry**、 **geography**  
  
-   CLR 用户定义的类型

通常，任何无法映射到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据类型的结果集都将输出为 NULL。  

### <a name="restrictions-specific-to-r"></a>专用于 R 的限制

如果输入包含的**日期时间**值不符合 R 中允许的值范围，则将值转换为**NA**。 这是必需的，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许比 R 语言支持的值范围更大的值。

尽管两种语言都使用 IEEE 754，但浮点值（例如 `+Inf`、`-Inf`、`NaN`）在 @no__t 中不受支持。 当前行为只是将值直接发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)];因此，[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的 SQL 客户端将引发错误。 因此，这些值将转换为**NULL**。

## <a name="permissions"></a>权限

需要**执行任何外部脚本**数据库权限。  

## <a name="examples"></a>示例

本部分包含有关如何使用此存储过程来执行使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的 R 或 Python 脚本的示例。

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. 将 R 数据集返回到 SQL Server  

下面的示例创建一个存储过程，该存储过程使用**sp_execute_external_script**将 R 中包含的 Iris 数据集返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  

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

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. 基于 SQL Server 中的数据生成 R 模型  

下面的示例创建一个存储过程，该存储过程使用**sp_execute_external_script**生成 iris 模型并将模型返回到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  

> [!NOTE]
>  此示例需要预先安装 e1071 包。 有关详细信息，请参阅[SQL Server 上的安装其他 R 包](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)。

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

Python 代码中使用的列标题不会输出到 SQL Server;因此，请使用 WITH RESULT 语句来指定要使用的 SQL 的列名称和数据类型。

要进行评分，还可以使用本机 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 函数，此函数无需调用 Python 或 R 运行时，因此更加快速。

## <a name="see-also"></a>请参阅

 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Python 库和数据类型](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [R 库和 R 数据类型](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)   
 [SQL Server 机器学习服务的已知问题](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
 [CREATE EXTERNAL LIBRARY &#40;transact-sql&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [external scripts enabled 服务器配置选项](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)   
 [SQL Server - External Scripts 对象](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
