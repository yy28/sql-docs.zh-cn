---
title: "sp_execute_external_script (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs: TSQL
helpviewer_keywords: sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d437e6e8d86aa648d9c6ef11a8ca04297cafbaf3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  执行作为在外部位置的自变量提供的脚本。 必须在支持并已注册的语言中编写脚本。 通过控制查询目录树[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用户无法执行基于该查询的任意操作。 若要执行**sp_execute_external_script**，必须先通过使用启用外部脚本`sp_configure 'external scripts enabled', 1;`语句。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_execute_external_script   
    @language = N'language,   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]   
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```  
  
## <a name="arguments"></a>参数  
 @language= N'*语言*  
 指示的脚本语言。 *语言*是**sysname**。  

 有效值为`Python`或`R`。 
  
 @script= N'*脚本*  
 外部语言指定为文字或变量输入脚本。 *脚本*是**nvarchar (max)**。  
  
 [ @input_data_1_name = N'*input_data_1_name*']  
 指定用于表示所定义的查询的变量的名称@input_data_1。 外部脚本中的变量的数据类型取决于的语言。 如果 R，则输入的变量是数据帧。 对于 Python，输入必须是表格。 *input_data_1_name*是**sysname**。  
  
 默认值为"InputDataSet"。  
  
 [ @input_data_1 = N'*input_data_1*']  
 指定使用的窗体中的外部脚本的输入的数据[!INCLUDE[tsql](../../includes/tsql-md.md)]查询。 *input_data_1*是**nvarchar (max)**。  
  
 [ @output_data_1_name = N'*output_data_1_name*']  
 指定的变量名称中包含要返回到的数据的外部脚本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的存储的过程调用完成后。 外部脚本中的变量的数据类型取决于的语言。 对于 R，输出必须属于数据帧。 对于 Python，输出必须属于 pandas 数据帧。 *output_data_1_name*是**sysname**。  
  
 默认值为"OutputDataSet"。  
  
 [ @parallel = 0 | 1 ]  
 通过设置启用并行执行 R 脚本`@parallel`为 1 的参数。 此参数的默认值为 0 (无 parallelism)。  
  
 为不使用 RevoScaleR 函数，请使用的 R 脚本`@parallel`参数可用于处理大型数据集，假定该脚本可以完全无法并行化有益。 例如，使用 R 时`predict`具有一个模型来生成新预测，设置函数`@parallel = 1`作为对查询引擎的提示。 如果查询可并行化，根据分发行**MAXDOP**设置。  
  
 如果`@parallel = 1`和输出正在进行数据流处理直接向客户端计算机，则`WITH RESULTS SETS`子句是必需的并且必须指定一个输出架构。  
  
 使用 RevoScaleR 函数的 R 脚本，并行处理处理自动，并且不应指定`@parallel = 1`到**sp_execute_external_script**调用。  
  
 [ @params = N' *@parameter_name data_type* [出 |输出] [，...n]']  
 该外部脚本中使用的输入的参数声明的列表。  
  
 [ @parameter1 =*value1*[出 |输出] [，...n]]  
 外部脚本使用的输入参数的值列表。  


## <a name="remarks"></a>注释  
 使用 **sp_execute_external_script** 执行受支持的语言（如 R）编写的脚本。在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中， [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 由与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一起安装的服务器组件工作站工具集和将数据科学家与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]高性能环境相连的连接库构成。 在过程中安装 R Services （数据库）[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序以启用 R 脚本的执行。 有关详细信息，请参阅[设置 SQL Server R Services &#40; 数据库中 &#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。  
  
 你可以控制通过配置的外部资源池使用的外部脚本的资源。 有关详细信息，请参阅 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。 从资源调控器目录视图、 DMV 的和计数器，可以获取有关工作负载的信息。 有关详细信息，请参阅[资源调控器目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)，[资源调控器相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)，和[SQL Server，外部脚本对象](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)。  

监视器脚本执行使用[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)和[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)。 

 默认情况下，此存储过程返回的结果集是使用未命名的列的输出。 使用的脚本中的列名称仅用于脚本编写环境，并不会反映在输出的结果集。 若要命名结果集列，使用`WITH RESULTS SET`子句[ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md)。
  
 除了返回的结果集，你可以从 R 脚本保存到返回标量值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用输出参数。 下面的示例演示了利用输出参数：  
  
```  
DECLARE @model varbinary(max);  
EXEC sp_execute_external_script  
        @language = N'R'  
        , @script = N'  
    # build classification model to predict tipped or not  
    logitObj <- glm(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource, family = binomial(link=logit));  
  
    # First, serialize a model and put it into a database table  
    modelbin <- serialize(logitObj, NULL);  
    '  
        , @input_data_1 = N'  
SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance  
  FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)  
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d  
'  
        , @input_data_1_name = N'featureDataSource'  
        , @params = N'@modelbin varbinary(max) OUTPUT'  
        , @modelbin = @model OUTPUT;  
```  


## <a name="streaming-execution-for-r-script"></a>流式处理 R 脚本的执行  
 通过指定支持流处理的 R 脚本执行`@r_rowsPerRead int parameter`中`@params`集合。  流处理使 R 脚本处理无法放在内存中的数据。 例如，如果有 100 亿行，以使用评分预测函数新`@r_rowsPerRead`参数可以用于拆分到一个流执行一次。 因为此参数控制发送到 R 进程的行数，它还可限制一次读取的行数。 这可能会降低服务器性能问题，如果，例如，定型一个大的模型很有用。 请注意，在此参数，仅可以在其中 R 脚本的输出不依赖于读取或查看整个行集的情况下使用。  
  
 这两个`@r_rowsPerRead`流式处理的参数和`@parallel`自变量应视为提示。 对于要应用的提示，它必须能生成包括并行处理的 SQL 查询计划。 如果这不是可能的不能启用并行处理。  
  
> [!NOTE]  
>  仅在 Enterprise Edition 中支持流式处理和并行处理。 你可以在标准版在查询中包含参数，而不会引发错误，但参数具有任何作用，而且在单个进程中运行的 R 脚本。  
  
## <a name="restrictions"></a>限制  
 **数据类型：**输入的查询或参数中使用时不支持以下数据类型`sp_execute_external_script`过程中，并返回不支持的类型错误。  
  
 一种解决方法，**强制转换**的列或值中的受支持类型[!INCLUDE[tsql](../../includes/tsql-md.md)]并将其发送到。  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**， **datetimeoffset**，**时间**  
  
-   **sql_variant**  
  
-   **文本**，**映像**  
  
-   **xml**  
  
-   **hierarchyid**，**几何图形**，**地理位置**  
  
-   CLR 用户定义的类型  
  
 **datetime**输入中的值的一侧 R 中。 这是必需的因为不适合的值的允许范围的值转换为 NA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]允许的值不是 R 语言中支持更大的范围。  
  
 中不支持 （有关示例，+ Inf、-Inf、 NaN） 的浮点值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]即使这两种语言使用 IEEE 754。 当前行为只需将值发送至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]直接，作为结果 sqlclient 在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]将引发错误。 这些值将转换为**NULL**。  
  
 无法映射到任何 R 结果集[!INCLUDE[tsql](../../includes/tsql-md.md)]数据类型，则输出为 NULL。  
  
## <a name="permissions"></a>Permissions  
 需要**执行任意外部脚本**数据库权限。  
  
## <a name="examples"></a>示例  
 本节包含演示如何使用此存储的过程以执行 R 脚本使用的示例[!INCLUDE[tsql](../../includes/tsql-md.md)]。  
  
### <a name="a-return-a-data-set-from-r-to-sql-server"></a>A. 从 R 到 SQL Server 返回数据集  
 下面的示例创建使用的存储的过程**sp_execute_external_script**从 R 到返回 iris 数据集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
```  
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
go  
```  
  
### <a name="b-generate-a-model-based-on-data-from-sql-server"></a>B. 生成基于从 SQL Server 的数据的模型  
 下面的示例创建使用的存储的过程**sp_execute_external_script**生成 iris 模型并返回到模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  此示例需要安装 e1071 包。 有关详细信息，请参阅[SQL Server 上安装其他 R 包](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)。  
  
```  
DROP PROC IF EXISTS generate_iris_model;  
go  
  
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
go  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Python 库和数据类型](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [R 库和 R 数据类型](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [SQL Server R Services 的已知的问题](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [创建外部库 &#40;Transact SQL &#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [启用了外部脚本的服务器配置选项](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)   
 [SQL Server - External Scripts 对象](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
  
