---
title: sp_execute_external_script（转算-SQL） |微软文档
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
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "80663015"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**sp_execute_external_script**存储过程执行作为过程的输入参数提供的脚本，并与[机器学习服务和](../../machine-learning/index.yml)[语言扩展](../../language-extensions/language-extensions-overview.md)一起使用。 

对于机器学习服务[，Python](../../machine-learning/concepts/extension-python.md)和[R](../../machine-learning/concepts/extension-r.md)是支持的语言。 对于语言扩展，Java 是支持的，但必须使用[创建外部语言](../../t-sql/statements/create-external-language-transact-sql.md)进行定义。

要执行**sp_execute_external_script**，必须首先安装机器学习服务或语言扩展。 有关详细信息，请参阅在 Windows 和[Linux](../../linux/sql-server-linux-setup-machine-learning.md)[上安装 SQL 服务器机器学习服务 （Python 和 R），](../../machine-learning/install/sql-machine-learning-services-windows-install.md)或在 Windows 和[Linux](../../linux/sql-server-linux-setup-language-extensions.md)上安装[SQL 服务器语言扩展](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md)。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
**sp_execute_external_script**存储过程执行作为过程的输入参数提供的脚本，并在 SQL Server 2017 上与[机器学习服务](../../machine-learning/index.yml)一起使用。 

对于机器学习服务[，Python](../../machine-learning/concepts/extension-python.md)和[R](../../machine-learning/concepts/extension-r.md)是支持的语言。 

要执行**sp_execute_external_script**，必须首先安装机器学习服务。 有关详细信息，请参阅在[Windows 上安装 SQL 服务器机器学习服务（Python 和 R）。](../../machine-learning/install/sql-machine-learning-services-windows-install.md)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**sp_execute_external_script**存储过程执行作为过程的输入参数提供的脚本，并在 SQL Server 2016 上与[R 服务](../../machine-learning/r/sql-server-r-services.md)一起使用。

对于 R 服务[，R](../../machine-learning/concepts/extension-r.md)是支持的语言。

要执行**sp_execute_external_script**，必须首先安装 R 服务。 有关详细信息，请参阅在[Windows 上安装 SQL 服务器机器学习服务（Python 和 R）。](../../machine-learning/install/sql-r-services-windows-install.md)
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
## <a name="syntax-for-2017-and-earlier"></a>2017 年及更早版本语法

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

## <a name="arguments"></a>自变量
 语言 = N'*语言*' ** \@**  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 指示脚本语言。 *语言*是**sysname**。 有效值为**R** **、Python**和使用[创建外部语言](../../t-sql/statements/create-external-language-transact-sql.md)（例如 Java）定义的任何语言。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 指示脚本语言。 *语言*是**sysname**。 在 SQL Server 2017 中，有效值为**R**和**Python**。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 指示脚本语言。 *语言*是**sysname**。 在 SQL Server 2016 中，唯一有效的值是**R**。
::: moniker-end

 脚本 = N'*脚本*" 外部语言脚本指定为文本或变量输入。 ** \@** *脚本*是**nvarchar（最大值）。**  

`[ @input_data_1 =  N'input_data_1' ]`以[!INCLUDE[tsql](../../includes/tsql-md.md)]查询的形式指定外部脚本使用的输入数据。 *input_data_1*的数据类型为**nvarchar（最大值）。**

`[ @input_data_1_name = N'input_data_1_name' ]`指定用于表示 定义的查询的@input_data_1变量的名称。 外部脚本中变量的数据类型取决于语言。 在 R 的情况下，输入变量是数据框。 在 Python 的情况下，输入必须为表格。 *input_data_1_name*是**sysname**。  默认值为*InputDataSet*。  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]`用于构建每个分区模型。 指定用于对结果集进行排序的列的名称，例如按产品名称。 外部脚本中变量的数据类型取决于语言。 在 R 的情况下，输入变量是数据框。 在 Python 的情况下，输入必须为表格。

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]`用于构建每个分区模型。 指定用于分割数据的列的名称，例如地理区域或日期。 外部脚本中变量的数据类型取决于语言。 在 R 的情况下，输入变量是数据框。 在 Python 的情况下，输入必须为表格。 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]`指定外部脚本中变量的名称，该变量包含完成存储过程调用后要返回到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的数据。 外部脚本中变量的数据类型取决于语言。 对于 R，输出必须是数据框。 对于 Python，输出必须是熊猫数据框。 *output_data_1_name*是**sysname**。  默认值为*输出数据集*。  

`[ @parallel = 0 | 1 ]`通过将参数设置为 1，实现 R`@parallel`脚本的并行执行。 此参数的默认值为 0（无并行性）。 如果`@parallel = 1`输出直接流式传输到客户端计算机，则需要子`WITH RESULT SETS`句，并且必须指定输出架构。  

 + 对于不使用 RevoScaleR 函数的 R 脚本，`@parallel`使用 参数可用于处理大型数据集，前提是脚本可以进行细微的并行化。 例如，将 R`predict`函数与模型一起使用以生成新预测时，`@parallel = 1`将设置为查询引擎的提示。 如果查询可以并行化，则根据**MAXDOP**设置分配行。  
  
 + 对于使用 RevoScaleR 函数的 R 脚本，并行处理会自动处理，并且`@parallel = 1`不应指定到**sp_execute_external_script**调用。  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]`外部脚本中使用的输入参数声明的列表。  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]`外部脚本使用的输入参数的值列表。  

## <a name="remarks"></a>备注

> [!IMPORTANT]
> 查询树由 该[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]树控制，用户无法对查询执行任意操作。 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
使用**sp_execute_external_script**执行使用受支持的语言编写的脚本。 支持的语言是与机器学习服务一起使用的**Python**和**R，** 以及使用["创建外部语言](../../t-sql/statements/create-external-language-transact-sql.md)"（例如 Java）定义的任何与语言扩展一起使用的语言。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
使用**sp_execute_external_script**执行使用受支持的语言编写的脚本。 支持的语言是 SQL Server 2017 机器学习服务中的**Python**和**R。**
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
使用**sp_execute_external_script**执行使用受支持的语言编写的脚本。 唯一支持的语言是 SQL Server 2016 R 服务中的**R。**
::: moniker-end

默认情况下，此存储过程返回的结果集使用未命名的列进行输出。 脚本中使用的列名称是脚本环境的本地名称，不会反映在输出结果集中。 要命名结果集列，`WITH RESULT SET`请使用 子[`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md)句。

除了返回结果集外，您还可以使用 OUTPUT 参数将标量值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回到 。 
  
您可以通过配置外部资源池来控制外部脚本使用的资源。 有关详细信息，请参阅[创建外部资源池&#40;处理-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。 有关工作负载的信息可以从资源调控器目录视图、DMV 和计数器获取。 有关详细信息，请参阅[资源调控器目录视图&#40;Transact-SQL&#41;、](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)[资源调控器相关动态管理视图&#40;处理-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)）和[SQL Server、外部脚本对象](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)。  

### <a name="monitor-script-execution"></a>监视脚本执行

使用[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)和[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)监视脚本执行。 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>分区建模的参数

您可以设置两个附加参数，以便在分区数据上启用建模，其中分区基于您提供的一个或多个列，这些列自然地将数据集段段到仅在脚本执行期间创建和使用的逻辑分区中。 包含年龄、性别、地理区域、日期或时间的重复值的列是适合分区数据集的几个示例。
 
这两个参数是**input_data_1_partition_by_columns**和**input_data_1_order_by_columns**，其中第二个参数用于对结果集进行排序。 参数作为输入传递给每个`sp_execute_external_script`分区的外部脚本一次。 有关详细信息和示例，请参阅[教程：创建基于分区的模型](https://docs.microsoft.com/sql/machine-learning/tutorials/r-tutorial-create-models-per-partition)。

可以通过指定`@parallel=1`并行执行脚本。 如果输入查询可以并行化，则应将作为参数的`@parallel=1`一部分设置为`sp_execute_external_script`。 默认情况下，查询优化器在具有 256 行以上的表下`@parallel=1`运行，但如果要显式处理此参数，此脚本将参数作为演示。

> [!Tip]
> 对于训练工作负载，可以将 `@parallel` 用于任意训练脚本，甚至是那些使用非 Microsoft-rx 算法的脚本。 通常，只有 RevoScaleR 算法（带有 rx 前缀）支持在 SQL Server 的训练方案中并行执行。 但是，使用 SQL Server vNext 中的新参数，您可以并行化调用未专门设计此功能的功能的脚本。
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Python 和 R 脚本的流式处理  

流式处理允许 Python 或 R 脚本处理比内存中容纳的数据多的数据。 要控制流式处理期间传递的行数，请在`@r_rowsPerRead``@params`集合中为参数指定整数值。  例如，如果您正在训练使用非常宽数据的模型，则可以调整该值以读取更少的行，以确保所有行都可以在一个数据块中发送。 您还可以使用此参数管理一次读取和处理的行数，以缓解服务器性能问题。 
  
流和`@r_rowsPerRead``@parallel`参数的参数都应视为提示。 要应用提示，必须可以生成包含并行处理的 SQL 查询计划。 如果无法这样做，则无法启用并行处理。  
  
> [!NOTE]  
> 流和并行处理仅在企业版中支持。 您可以在标准版的查询中包括参数，而不会引发错误，但参数不起作用，R 脚本在单个进程中运行。  
  
## <a name="restrictions"></a>限制  

### <a name="data-types"></a>数据类型

在输入查询或**sp_execute_external_script**过程的参数中使用时，不支持以下数据类型，并返回不支持的类型错误。  

作为解决方法，在将其**CAST**发送到外部脚本[!INCLUDE[tsql](../../includes/tsql-md.md)]之前，将列或值强制转换为受支持的类型。  
  
-   **光标**  
  
-   **timestamp**  
  
-   **日期时间2**，**日期时间偏移**，**时间**  
  
-   **sql_variant**  
  
-   **文本**，**图像**  
  
-   **xml**  
  
-   **层次结构**，**几何 ，****地理**  
  
-   CLR 用户定义的类型

通常，任何无法映射到[!INCLUDE[tsql](../../includes/tsql-md.md)]数据类型的结果集都输出为 NULL。  

### <a name="restrictions-specific-to-r"></a>特定于 R 的限制

如果输入包括的日期**时间**值不符合 R 中允许的值范围，则值将转换为**NA**。 这是必需的，因为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]允许的值范围比 R 语言中支持的值范围更大。

即使两种语言都使用`+Inf`IEEE 754，也不支持浮点值（例如 ， `-Inf`， `NaN`， 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 当前行为只是将值直接发送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)];因此，中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]SQL 客户端会引发错误。 因此，这些值将转换为**NULL**。

## <a name="permissions"></a>权限

需要**执行任何外部脚本**数据库权限。  

## <a name="examples"></a>示例

本节包含如何使用此存储过程使用 执行 R 或 Python 脚本的示例[!INCLUDE[tsql](../../includes/tsql-md.md)]。

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. 将 R 数据集返回到 SQL 服务器  

下面的示例创建一个存储过程，使用**sp_execute_external_script**将 R 中包含的 Iris 数据集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回到 。  

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

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. 基于 SQL Server 的数据生成 R 模型  

下面的示例创建一个存储过程，该过程使用**sp_execute_external_script**生成光圈模型并将模型返回到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  

> [!NOTE]
>  此示例要求提前安装 e1071 软件包。 有关详细信息，请参阅在[SQL Server 上安装其他 R 包](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)。

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

Python 代码中使用的列标题不会输出到 SQL Server;但是，这些列标题不会输出到 SQL Server。因此，使用 WITH RESULT 语句指定要使用的 SQL 的列名称和数据类型。

要进行评分，还可以使用本机 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 函数，此函数无需调用 Python 或 R 运行时，因此更加快速。

## <a name="see-also"></a>请参阅

+ [SQL 服务器机器学习服务](../../machine-learning/index.yml)
+ [SQL 服务器语言扩展](../../language-extensions/language-extensions-overview.md)。 
+ [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [Python 库和数据类型](../../machine-learning/python/python-libraries-and-data-types.md)  
+ [R 库和 R 数据类型](../../machine-learning/r/r-libraries-and-data-types.md)  
+ [SQL 服务器 R 服务](../../machine-learning/r/sql-server-r-services.md)   
+ [SQL 服务器机器学习服务的已知问题](../../machine-learning/known-issues-for-sql-server-machine-learning-services.md)   
+ [创建外部库&#40;转接-SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [sp_prepare&#40;交易 SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [启用了外部脚本的服务器配置选项](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [SQL Server - External Scripts 对象](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
