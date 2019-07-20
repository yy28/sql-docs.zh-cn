---
title: R 到 SQL 数据类型转换
description: 查看数据科学和机器学习解决方案中 R 与 SQL Server 之间的隐式和显式数据类型 converstions。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 255342113a17b0fb2af58eb6bc173cb6c50aac6d
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344933"
---
# <a name="data-type-mappings-between-r-and-sql-server"></a>R 与 SQL Server 之间的数据类型映射
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

对于在 SQL Server 机器学习服务中的 R 集成功能上运行的 R 解决方案, 请查看不支持的数据类型的列表, 以及在 R 库和 SQL Server 之间传递数据时可能隐式执行的数据类型转换。

## <a name="base-r-version"></a>基本 R 版本

SQL Server 2016 R Services 和 SQL Server 2017 机器学习服务 with R, 与 Microsoft R Open 的特定版本保持一致。 例如, 最新版本 SQL Server 2017 机器学习服务在 Microsoft R Open 3.3.3 上构建。

若要查看与 SQL Server 的特定实例关联的 R 版本, 请打开**rgui.exe**。 对于默认实例, 路径将如下所示:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64\`

此工具将加载基本 R 和其他库。 在会话启动时加载的每个包的通知中提供了包版本信息。 

## <a name="r-and-sql-data-types"></a>R 和 SQL 数据类型

虽然[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持数十个数据类型, 但 R 的标量数据类型 (数字、整数、复杂、逻辑、字符、日期/时间和原始) 数量有限。 因此, 每次使用 R 脚本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的数据时, 数据可能会隐式转换为兼容的数据类型。 但是, 通常不能自动执行精确转换, 而是返回错误, 如 "未处理的 SQL 数据类型"。

本节列出了提供的隐式转换, 并列出了不受支持的数据类型。 为在 R 和 SQL Server 之间映射数据类型提供了一些指导。

## <a name="implicit-data-type-conversions-between-r-and-sql-server"></a>R 与 SQL Server 之间的隐式数据类型转换

下表显示了当来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的数据在 R 脚本中使用，然后返回到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，数据类型和值中的变化。

|SQL 类型|R 类|RESULT SET 类型|注释|
|-|-|-|-|
|**bigint**|`numeric`|**float**||
|**binary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|仅允许作为输入参数和输出|
|**bit**|`logical`|**bit**||
|**char(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||
|**datetime**|`POSIXct`|**datetime**|表示为 GMT|
|**date**|`POSIXct`|**datetime**|表示为 GMT|
|**decimal(p,s)**|`numeric`|**float**||
|**float**|`numeric`|**float**||
|**int**|`integer`|**int**||
|**money**|`numeric`|**float**||
|**numeric(p,s)**|`numeric`|**float**||
|**real**|`numeric`|**float**||
|**smalldatetime**|`POSIXct`|**datetime**|表示为 GMT|
|**smallint**|`integer`|**int**||
|**smallmoney**|`numeric`|**float**||
|**tinyint**|`integer`|**int**||
|**uniqueidentifier**|`character`|**varchar(max)**||
|**varbinary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|仅允许作为输入参数和输出|
|**varbinary(max)**|`raw`|**varbinary(max)**|仅允许作为输入参数和输出|
|**varchar(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||


## <a name="data-types-not-supported-by-r"></a>R 不支持的数据类型

在 [SQL Server 类型系统](../../t-sql/data-types/data-types-transact-sql.md)支持的数据类型类别中，如果将以下类型传递给 R 代码，则有可能会造成问题：

+ SQL 类型系统文章的**另**一部分中列出的数据类型: **cursor**、 **timestamp**、 **hierarchyid**、 **uniqueidentifier**、 **sql_variant**、 **xml**、 **table**
+ 所有空间类型
+ **image**

## <a name="data-types-that-might-convert-poorly"></a>转换结果可能不佳的数据类型

+ 除 **datetimeoffset** 以外的大多数 datetime 类型应可正常转换 
+ 支持大部分数字数据类型，但 **money** 和**smallmoney** 的转换可能会失败
+ 支持 **varchar**，但由于 SQL Server 往往使用 Unicode，因此，我们建议尽量使用 **nvarchar** 和其他 Unicode 文本数据类型。
+ RevoScaleR 库中带有 rx 前缀的函数可以处理 SQL 二进制数据类型（**binary** 和 **varbinary**），但大多数情况下，需要对这些类型进行特殊处理。 大多数 R 代码无法处理二进制列。

  
 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型的详细信息，请参阅[数据类型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。

## <a name="changes-in-data-types-between-sql-server-2016-and-earlier-versions"></a>SQL Server 2016 与早期版本中数据类型的变化

Microsoft SQL Server 2016 和 Microsoft Azure SQL 数据库对数据类型转换和其他一些操作做了改进。 其中的大多数改进都提高了处理浮点类型时的精度，同时对经典 **datetime** 类型的操作做了轻微的改变。

使用 130 或更高的数据库兼容级别时，默认会使用这些改进。 但是，如果使用不同的兼容级别，或者使用旧版本连接到数据库，可能会看到数字精度的变化或其他结果。 

有关详细信息，请参阅 [SQL Server 2016 improvements in handling some data types and uncommon operations](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon-)（SQL Server 2016 在处理某些数据类型和不常见操作方面所做的改进）。
 

## <a name="verify-r-and-sql-data-schemas-in-advance"></a>提前验证 R 和 SQL 数据架构 

一般情况下，每当你对特定的数据类型或数据结构在 R 中如何使用有疑问时，请使用  `str()` 函数获取 R 对象的内部结构和类型。 函数的结果将打印到 R 控制台，并且也在 **中的“消息”** [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]选项卡中的查询结果中可用。 

当从数据库中检索数据以用于 R 代码时, 应始终消除不能在 R 中使用的列以及对于分析不有用的列, 例如 GUID (uniqueidentifier)、时间戳和用于审核的其他列, 或沿袭ETL 进程创建的信息。 

请注意，包含不必要的列可以会极大降低 R 代码的性能，尤其是将高基数列用作因子时。 因此，我们建议使用 SQL Server 系统存储过程和信息视图来提前获取给定表的数据类型，并消除或转换不兼容的列。 有关详细信息，请参阅 [Information Schema Views in Transact-SQL](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)（Transact-SQL 中的信息架构视图）

如果某个特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型不受 R 支持，但你需要在 R 脚本中使用数据列，我们建议在 R 脚本中使用这些数据之前，使用 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md) 函数确保数据类型转换按预期执行。  

> [!WARNING]
> 如果在移动数据时使用 **rxDataStep** 删除不兼容的列，请注意，**RxSqlServerData** 数据源类型不支持 _varsToKeep_ 和 _varsToDrop_ 参数。


## <a name="examples"></a>示例

### <a name="example-1-implicit-conversion"></a>示例 1：隐式转换

以下示例演示在 SQL Server 与 R.之间往返访问时如何转换数据。

此查询从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表中获取一系列值, 并使用存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)输出使用 R 运行时的值。

```sql
CREATE TABLE MyTable (    
 c1 int,    
 c2 varchar(10),    
 c3 uniqueidentifier    
);    
go    
INSERT MyTable VALUES(1, 'Hello', newid());    
INSERT MyTable VALUES(-11, 'world', newid());    
SELECT * FROM MyTable;    
  
EXECUTE sp_execute_external_script    
 @language = N'R'    
 , @script = N'    
inputDataSet["cR"] <- c(4, 2)    
str(inputDataSet)    
outputDataSet <- inputDataSet'    
 , @input_data_1 = N'SELECT c1, c2, c3 FROM MyTable'    
 , @input_data_1_name = N'inputDataSet'    
 , @output_data_1_name = N'outputDataSet'    
 WITH RESULT SETS((C1 int, C2 varchar(max), C3 varchar(max), C4 float));  
```

**结果**

||||||
|-|-|-|-|-|
||C1|C2|C3|C4|
|1|1|Hello|6e225611-4b58-4995-a0a5-554d19012ef1|4|
|1|-11|world|6732ea46-2d5d-430b-8ao1-86e7f3351c3e|2|

注意使用 R 中的 `str` 函数可获取输出数据的架构。 此函数返回以下信息：

<code>'data.frame':2 obs. of  4 variables:</code>
<code> $ c1: int  1 -11</code>
<code> $ c2: Factor w/ 2 levels "Hello","world": 1 2</code>
<code> $ c3: Factor w/ 2 levels "6732EA46-2D5D-430B-8A01-86E7F3351C3E",..: 2 1</code>
<code> $ cR: num  4 2</code>

由此，可以看到下面的数据类型转换作为此查询的一部分隐式地执行：

-   **列 C1**。 列被表示为 **ssNoversion** 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、R 中的 `integer` 和输出结果集中的 **ssNoversion** 。  
  
     未执行任何类型转换。  
  
-   **列 C2**。 列被表示为 **ssNoversion** 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、R 中的 `factor` 和输出结果集中的 **varchar(max)** 。  
  
     注意输出如何变化；R 中的任何字符串（因子或常规字符串）将被表示为 **varchar(max)** ，不论字符串的长度为多少。  
  
-   **列 C3**。  列被表示为 **ssNoversion** 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、R 中的 `character` 和输出结果集中的 **varchar(max)** 。
  
     注意发生的数据类型转换。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持 **ssNoversion** ，但 R 不支持；因此，标识符表示为字符串。
  
-   **列 C4**。 列包含由 R 脚本生成的值且不会出现在原始数据中。


## <a name="example-2-dynamic-column-selection-using-r"></a>示例 2：使用 R 的动态列选择

以下示例演示如何使用 R 代码来检查无效的列类型。 该查询使用 SQL Server 系统视图获取指定表的架构，然后删除指定的类型无效的所有列。

```R
connStr <- "Server=.;Database=TestDB;Trusted_Connection=Yes"
data <- RxSqlServerData(connectionString = connStr, sqlQuery = "SELECT COLUMN_NAME FROM TestDB.INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = N'testdata' AND DATA_TYPE <> 'image';")
columns <- rxImport(data)
columnList <- do.call(paste, c(as.list(columns$COLUMN_NAME), sep = ","))
sqlQuery <- paste("SELECT", columnList, "FROM testdata")
```

## <a name="see-also"></a>请参阅

