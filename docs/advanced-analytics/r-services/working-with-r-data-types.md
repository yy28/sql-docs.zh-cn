---
title: "使用 R 数据类型 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5df99e1c-a89a-42c1-9d68-ffe8d9577c94
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# 使用 R 数据类型
  而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持几种几十个数据类型，R 具有有限的数量的标量数据类型 (numeric、 整数、 复杂、 逻辑字符日期/时间和原始)。 因此，当在 R 脚本中使用来自  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的数据时，会发生几种不同的情况：  
  
-   数据隐式转换为兼容的数据类型。  
  
-   数据不能隐式转换，并将返回错误。  
  
 一般情况下，每当你对特定的数据类型或数据结构在 R 中如何使用有疑问时，请使用  `str()` 函数获取 R 对象的内部结构和类型。 函数的结果将打印到 R 控制台，并且也在 **中的“消息”**[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]选项卡中的查询结果中可用。  
  
 如果特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R，不支持数据类型，但您需要在 R 脚本中使用的数据列，我们建议你使用 [CAST 和 CONVERT & #40;Transact SQL & #41;](../../t-sql/functions/cast-and-convert-transact-sql.md) 运行安装程序，在 R 脚本中使用这些数据之前执行函数以确保数据类型转换。  
  
 有关详细信息 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型，请参阅 [数据类型和 #40;Transact SQL & #41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
## R 和 SQL Server 之间的数据类型转换  
 下表显示了当来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的数据在 R 脚本中使用，然后返回到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，数据类型和值中的变化。  
  
|||||  
|-|-|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型|R 类| **RESULT SET**中的类型|注释|  
|**smalldatetime**|`POSIXct`|**datetime**|表示为 GMT|  
|**smallmoney**|`numeric`|**float**||  
|**datetime**|`POSIXct`|**datetime**|表示为 GMT|  
|**money**|`numeric`|**float**||  
|**uniqueidentifier**|`character`|**varchar(max)**||  
|**numeric(p,s)**|`numeric`|**float**||  
|**decimal(p,s)**|`numeric`|**float**||  
|**date**|`POSIXct`|**datetime**|表示为 GMT|  
|**tinyint**|`integer`|**int**||  
|**bit**|`logical`|**bit**||  
|**smallint**|`integer`|**int**||  
|**int**|`integer`|**int**||  
|**float**|`numeric`|**float**||  
|**real**|`numeric`|**float**||  
|**bigint**|`numeric`|**float**||  
|**binary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|仅允许作为输入参数和输出|  
|**char(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||  
|**varbinary （n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|仅允许作为输入参数和输出|  
|**varchar （n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||  
|**varbinary(max)**|`raw`|**varbinary(max)**|仅允许作为输入参数和输出|  
  
## 数据类型转换的示例  
 以下查询获取的一系列值从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表，并使用存储的过程  [sp_execute_external_script & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 若要输出中使用 R 运行时的值。  
  
```  
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
  
```  
'data.frame':2 obs. of  4 variables:   
 $ c1: int  1 -11   
 $ c2: Factor w/ 2 levels "Hello","world": 1 2   
 $ c3: Factor w/ 2 levels "6732EA46-2D5D-430B-8A01-86E7F3351C3E",..: 2 1   
 $ cR: num  4 2  
```  
  
 由此，可以看到下面的数据类型转换作为此查询的一部分隐式地执行：  
  
-   **列 C1**。 列表示为 **int** 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ，`integer` 在 R 中，和 **int** 在输出结果集中。  
  
     未执行任何类型转换。  
  
-   **列 C2**。 列表示为 **varchar （10)** 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ，`factor` 在 R 中，和 **varchar （max)** 在输出中。  
  
     请注意输出如何发生变化;来自 R （一个因素或规则的字符串） 的任何字符串都表示为 **varchar （max)**, ，无论字符串的长度是什么。  
  
-   **列 C3**。  列表示为 **uniqueidentifier** 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ，`character` 在 R 中，和 **varchar （max)** 在输出中。  
  
     注意发生的数据类型转换。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持 **uniqueidentifier** ，但是 R 不; 因此，标识符表示为字符串。  
  
-   **列 C4**。 列包含由 R 脚本生成的值且不会出现在原始数据中。  
 
 ## 另请参阅
 [SQL Server R 服务功能和任务](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)
  
  