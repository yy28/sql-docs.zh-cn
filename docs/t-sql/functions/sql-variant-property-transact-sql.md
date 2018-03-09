---
title: "SQL_VARIANT_PROPERTY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SQL_VARIANT_PROPERTY_TSQL
- SQL_VARIANT_PROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- SQL_VARIANT_PROPERTY function
- sql_variant data type
ms.assetid: 50e5c1d9-4e95-4ed0-9c92-435c872a399e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5947528f4e8959de1b8b4ee3679d4e3e058476d5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sqlvariantproperty-transact-sql"></a>SQL_VARIANT_PROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回有关的基本数据类型和其他信息**sql_variant**值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SQL_VARIANT_PROPERTY ( expression , property )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 类型的表达式**sql_variant**。  
  
 *属性*  
 包含名称的**sql_variant**旨在提供信息的属性。 *属性*是**varchar (**128**)**，并且可以是以下值之一：  
  
|值|Description|返回的 sql_variant 基类型|  
|-----------|-----------------|----------------------------------------|  
|**BaseType**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型，例如：<br /><br /> **bigint**<br /><br /> **binary**<br /><br /> **char**<br /><br /> **date**<br /><br /> **datetime**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **int**<br /><br /> **money**<br /><br /> **nchar**<br /><br /> **numeric**<br /><br /> **nvarchar**<br /><br /> **real**<br /><br /> **smalldatetime**<br /><br /> **int**<br /><br /> **smallmoney**<br /><br /> **time**<br /><br /> **tinyint**<br /><br /> **uniqueidentifier**<br /><br /> **varbinary**<br /><br /> **varchar**|**sysname**<br /><br /> NULL = 输入无效。|  
|**精度**|数值基本数据类型的位数：<br /><br /> **datetime** = 23<br /><br /> **smalldatetime** = 16<br /><br /> **float** = 53<br /><br /> **实际**= 24<br /><br /> **十进制**（p、 s） 和**数值**（p、 s） = p<br /><br /> **money** = 19<br /><br /> **smallmoney** = 10<br /><br /> **bigint** = 19<br /><br /> **int** = 10<br /><br /> **smallint** = 5<br /><br /> **tinyint** = 3<br /><br /> **位**= 1<br /><br /> 所有其他类型 = 0|**int**<br /><br /> NULL = 输入无效。|  
|**小数位数**|数值基本数据类型的小数点后的位数：<br /><br /> **十进制**（p、 s） 和**数值**（p、 s） = s<br /><br /> **money**和**smallmoney** = 4<br /><br /> **datetime** = 3<br /><br /> 所有其他类型 = 0|**int**<br /><br /> NULL = 输入无效。|  
|**TotalBytes**|同时容纳值的元数据和数据所需的字节数。 此信息可用于检查中的数据的最大端**sql_variant**列。 如果值大于 900，索引创建将失败。|**int**<br /><br /> NULL = 输入无效。|  
|**排序规则**|表示特定的排序规则**sql_variant**值。|**sysname**<br /><br /> NULL = 输入无效。|  
|**MaxLength**|最大数据类型长度（字节）。 例如， **MaxLength**的**nvarchar (**50**)**为 100， **MaxLength**的**int**为 4。|**int**<br /><br /> NULL = 输入无效。|  
  
## <a name="return-types"></a>返回类型  
 **sql_variant**  
  
## <a name="examples"></a>示例  
### <a name="a-using-a-sqlvariant-in-a-table"></a>A. 表中使用 sql_variant  
 下面的示例检索`SQL_VARIANT_PROPERTY`有关的信息`colA`值`46279.1`其中`colB`  = `1689`，鉴于`tableA`具有`colA`类型`sql_variant`和`colB`.  
  
```sql    
CREATE   TABLE tableA(colA sql_variant, colB int)  
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)  
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',  
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',  
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'  
FROM      tableA  
WHERE      colB = 1689  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]请注意，其中每个三个值是**sql_variant**。  
  
```  
Base Type    Precision    Scale  
---------    ---------    -----  
decimal      8           2  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-a-sqlvariant-as-a-variable"></a>B. 使用 sql_variant 作为变量   
 下面的示例检索`SQL_VARIANT_PROPERTY`有关名为变量的信息@v1。  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```  
  
## <a name="see-also"></a>另请参阅  
 [sql_variant (Transact-SQL)](../../t-sql/data-types/sql-variant-transact-sql.md)  
  
  

