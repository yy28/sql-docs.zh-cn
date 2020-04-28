---
title: sp_execute_external_script （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
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
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 8800df26e505f1fffe25e6f65218481e7a8158f0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "80663015"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**Sp_execute_external_script**存储过程执行以输入参数形式提供给过程的脚本，并与[机器学习服务](../../machine-learning/index.yml)和[语言扩展](../../language-extensions/language-extensions-overview.md)一起使用。 

机器学习服务、 [Python](../../machine-learning/concepts/extension-python.md)和[R](../../machine-learning/concepts/extension-r.md)是受支持的语言。 对于语言扩展，Java 是支持的，但必须用[CREATE EXTERNAL Language](../../t-sql/statements/create-external-language-transact-sql.md)定义。

若要执行**sp_execute_external_script**，必须首先安装机器学习服务或语言扩展。 有关详细信息，请参阅在 Windows 和[linux](../../linux/sql-server-linux-setup-machine-learning.md)[上安装 SQL Server 机器学习服务（Python 和 R）](../../machine-learning/install/sql-machine-learning-services-windows-install.md) ，或在 Windows 和[Linux](../../linux/sql-server-linux-setup-language-extensions.md)[上安装 SQL Server 语言扩展](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md)。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
**Sp_execute_external_script**存储过程执行以输入参数形式提供给过程的脚本，并与 SQL Server 2017 上的[机器学习服务](../../machine-learning/index.yml)一起使用。 

机器学习服务、 [Python](../../machine-learning/concepts/extension-python.md)和[R](../../machine-learning/concepts/extension-r.md)是受支持的语言。 

若要执行**sp_execute_external_script**，必须先安装机器学习服务。 有关详细信息，请参阅[在 Windows 上安装 SQL Server 机器学习服务（Python 和 R）](../../machine-learning/install/sql-machine-learning-services-windows-install.md)。
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**Sp_execute_external_script**存储过程执行以输入参数形式提供给过程的脚本，并与 SQL Server 2016 上的[R Services](../../machine-learning/r/sql-server-r-services.md)一起使用。

对于 R 服务， [r](../../machine-learning/concepts/extension-r.md)是支持的语言。

若要执行**sp_execute_external_script**，你必须首先安装 R Services。 有关详细信息，请参阅[在 Windows 上安装 SQL Server 机器学习服务（Python 和 R）](../../machine-learning/install/sql-r-services-windows-install.md)。
::: moniker-end

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

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
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
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
 language = N "*language*" ** \@**  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 指示脚本语言。 *语言*为**sysname**。 有效值为**R**、 **Python**和通过[创建外部语言](../../t-sql/statements/create-external-language-transact-sql.md)（例如，Java）定义的任何语言。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 指示脚本语言。 *语言*为**sysname**。 在 SQL Server 2017 中，有效值为**R**和**Python**。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 指示脚本语言。 *语言*为**sysname**。 在 SQL Server 2016 中，唯一有效的值是**R**。
::: moniker-end

 script = N "*script*" 外部语言脚本指定为文本或变量输入。 ** \@** *脚本*为**nvarchar （max）**。  

`[ @input_data_1 =  N'input_data_1' ]`以[!INCLUDE[tsql](../../includes/tsql-md.md)]查询形式指定外部脚本使用的输入数据。 *Input_data_1*的数据类型为**nvarchar （max）**。

`[ @input_data_1_name = N'input_data_1_name' ]`指定用于表示由@input_data_1定义的查询的变量名称。 外部脚本中的变量的数据类型取决于语言。 对于 R，输入变量是数据帧。 对于 Python，输入必须为表格格式。 *input_data_1_name* **sysname**。  默认值为*InputDataSet*。  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]`用于生成每个分区的模型。 指定用于对结果集进行排序的列的名称，例如 "产品名称"。 外部脚本中的变量的数据类型取决于语言。 对于 R，输入变量是数据帧。 对于 Python，输入必须为表格格式。

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]`用于生成每个分区的模型。 指定用于对数据进行分段的列的名称，如地理区域或日期。 外部脚本中的变量的数据类型取决于语言。 对于 R，输入变量是数据帧。 对于 Python，输入必须为表格格式。 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]`指定包含在完成存储过程调用后要返回到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的数据的外部脚本中的变量的名称。 外部脚本中的变量的数据类型取决于语言。 对于 R，输出必须是数据帧。 对于 Python，输出必须为 pandas 数据帧。 *output_data_1_name* **sysname**。  默认值为*OutputDataSet*。  

`[ @parallel = 0 | 1 ]`通过将`@parallel`参数设置为1来启用对 R 脚本的并行执行。 此参数的默认值为0（无并行）。 如果`@parallel = 1`和输出正在直接流式传输到客户端计算机，则需要`WITH RESULT SETS`子句并且必须指定输出架构。  

 + 对于不使用 RevoScaleR 函数的 R 脚本，使用`@parallel`参数对于处理大型数据集非常有利，假设脚本可以完全并行化。 例如，使用带有模型的 R `predict`函数生成新的预测时，将设置`@parallel = 1`为查询引擎的提示。 如果可以并行化查询，行将按照**MAXDOP**设置进行分布。  
  
 + 对于使用 RevoScaleR 函数的 R 脚本，会自动处理并行处理，而不应指定`@parallel = 1` **sp_execute_external_script**调用。  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]`外部脚本中使用的输入参数声明的列表。  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]`外部脚本使用的输入参数的值列表。  

## <a name="remarks"></a>备注

> [!IMPORTANT]
> 查询树由控制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，用户无法对查询执行任意操作。 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
使用**sp_execute_external_script**执行使用支持的语言编写的脚本。 支持的语言是用于机器学习服务的**Python**和**R** ，以及使用[创建外部语言](../../t-sql/statements/create-external-language-transact-sql.md)（例如，Java）定义的任何语言，使用语言扩展。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
使用**sp_execute_external_script**执行使用支持的语言编写的脚本。 支持的语言为 SQL Server 2017 机器学习服务中的**Python**和**R** 。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
使用**sp_execute_external_script**执行使用支持的语言编写的脚本。 唯一受支持的语言是 SQL Server 2016 R Services 中的**r** 。
::: moniker-end

默认情况下，此存储过程返回的结果集是具有未命名列的输出。 脚本中使用的列名是脚本环境的本地列名，不会反映在输出结果集中。 若要命名结果集列，请`WITH RESULT SET`使用的[`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md)子句。

除了返回一个结果集之外，您还可以使用输出参数将[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标量值返回到。 
  
可以通过配置外部资源池来控制外部脚本所使用的资源。 有关详细信息，请参阅[CREATE EXTERNAL RESOURCE POOL &#40;transact-sql&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。 可从资源调控器目录视图、DMV 和计数器获取有关工作负荷的信息。 有关详细信息，请参阅[Resource Governor 目录视图 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)， [Resource Governor 相关的动态管理视图 &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)和[SQL Server 外部脚本对象](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)。  

### <a name="monitor-script-execution"></a>监视脚本执行

使用[sys. dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)和[dm_external_script_execution_stats sys.databases](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)监视脚本执行。 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>分区建模的参数

您可以设置两个附加参数，这些参数对分区数据启用建模，其中分区基于您提供的一个或多个列，这些列将数据集中的一个或多个列自然分段到仅在脚本执行过程中创建和使用的逻辑分区。 包含年龄、性别、地理区域、日期或时间的重复值的列是几个可用于分区数据集的示例。
 
这两个参数**input_data_1_partition_by_columns**和**input_data_1_order_by_columns**中，第二个参数用于对结果集进行排序。 参数作为输入传递给， `sp_execute_external_script`并为每个分区执行一次外部脚本。 有关详细信息和示例，请参阅[教程：创建基于分区的模型](https://docs.microsoft.com/sql/machine-learning/tutorials/r-tutorial-create-models-per-partition)。

可以通过指定`@parallel=1`并行执行脚本。 如果输入查询可并行化，则应将参数`@parallel=1`设置为的一部分`sp_execute_external_script`。 默认情况下，查询优化器在`@parallel=1`超过256行的表下运行，但如果想要显式处理此操作，则此脚本会将参数作为演示。

> [!Tip]
> 对于训练工作负载，可以将 `@parallel` 用于任意训练脚本，甚至是那些使用非 Microsoft-rx 算法的脚本。 通常，只有 RevoScaleR 算法（带有 rx 前缀）支持在 SQL Server 的训练方案中并行执行。 但使用 SQL Server vNext 中的新参数，可以并行化脚本，该脚本调用未使用该功能专门设计的函数。
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Python 和 R 脚本的流式执行  

使用流式处理时，Python 或 R 脚本可以处理的数据可能会超出内存量。 若要控制在流式处理期间传递的行数，请`@r_rowsPerRead`在`@params`集合中为该参数指定一个整数值。  例如，如果您在定型使用非常宽数据的模型，则可以调整该值以读取较少的行，以确保所有行都可以在一个数据块中发送。 你还可以使用此参数来管理一次读取和处理的行数，以减少服务器性能问题。 
  
用于流式`@r_rowsPerRead`处理的参数和`@parallel`参数均应视为提示。 若要应用提示，必须能够生成包含并行处理的 SQL 查询计划。 如果这是不可能的，则不能启用并行处理。  
  
> [!NOTE]  
> 只有 Enterprise Edition 支持流式处理和并行处理。 你可以在标准版的查询中包含参数，而不会引发错误，但参数不起作用，并且 R 脚本在单个进程中运行。  
  
## <a name="restrictions"></a>限制  

### <a name="data-types"></a>数据类型

在**sp_execute_external_script**过程的输入查询或参数中使用时，不支持以下数据类型，并返回不支持的类型错误。  

解决方法是将列或值**转换**为中[!INCLUDE[tsql](../../includes/tsql-md.md)]的支持类型，然后再将其发送到外部脚本。  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**、 **datetimeoffset**、 **time**  
  
-   **sql_variant**  
  
-   **文本**、**图像**  
  
-   **xml**  
  
-   **hierarchyid**、 **geometry**、 **geography**  
  
-   CLR 用户定义的类型

通常，任何无法映射到[!INCLUDE[tsql](../../includes/tsql-md.md)]数据类型的结果集都将输出为 NULL。  

### <a name="restrictions-specific-to-r"></a>专用于 R 的限制

如果输入包含的**日期时间**值不符合 R 中允许的值范围，则将值转换为**NA**。 这是必需的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，因为允许使用比 R 语言支持的值更大的值范围。

尽管这两种语言都`+Inf`使用`-Inf`IEEE `NaN`754，但浮点值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （例如，、、）在中不受支持。 当前行为直接向[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]直接发送值;因此，中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的 SQL 客户端将引发错误。 因此，这些值将转换为**NULL**。

## <a name="permissions"></a>权限

需要**执行任何外部脚本**数据库权限。  

## <a name="examples"></a>示例

本部分包含有关如何使用此存储过程来执行 R 或 Python 脚本的示例[!INCLUDE[tsql](../../includes/tsql-md.md)]。

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. 将 R 数据集返回到 SQL Server  

下面的示例创建一个存储过程，该存储过程使用**sp_execute_external_script**返回 R 所包含的 Iris [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据集。  

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

下面的示例创建一个存储过程，该存储过程使用**sp_execute_external_script**生成 iris 模型并将模型返回[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到。  

> [!NOTE]
>  此示例需要预先安装 e1071 包。 有关详细信息，请参阅[SQL Server 上的安装其他 R 包](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)。

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

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. 创建 Python 模型并通过该模型生成分数

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

## <a name="see-also"></a>另请参阅

+ [SQL Server 机器学习服务](../../machine-learning/index.yml)
+ [SQL Server 语言扩展](../../language-extensions/language-extensions-overview.md)。 
+ [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [Python 库和数据类型](../../machine-learning/python/python-libraries-and-data-types.md)  
+ [R 库和 R 数据类型](../../machine-learning/r/r-libraries-and-data-types.md)  
+ [SQL Server R Services](../../machine-learning/r/sql-server-r-services.md)   
+ [SQL Server 机器学习服务的已知问题](../../machine-learning/known-issues-for-sql-server-machine-learning-services.md)   
+ [CREATE EXTERNAL LIBRARY &#40;Transact-sql&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [sp_prepare &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [“已启用外部脚本”服务器配置选项](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [SQL Server - External Scripts 对象](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
