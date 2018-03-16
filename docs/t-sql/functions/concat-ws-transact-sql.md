---
title: CONCAT_WS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CONCAT_WS
- CONCAT_WS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_WS function
ms.assetid: f1375fd7-a2fd-48bf-922a-4f778f0deb1f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7d7932c1887c82b2a10702f9054706e4cf9bce71
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

使用第 1 个参数中指定的分隔符连接可变数量的参数。 （`CONCAT_WS` 指示使用分隔符连接。）

##  <a name="syntax"></a>语法   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>参数   
separator  
任何字符类型的表达式（`nvarchar`、`varchar``nchar` 或 `char`）。

argument1、argument2、argumentN  
是任何类型的表达式。

## <a name="return-types"></a>返回类型
字符串。 长度和类型取决于输入。

## <a name="remarks"></a>Remarks   
`CONCAT_WS` 采用可变数量的参数，并使用第一个参数作为分隔符将它们连接成单个字符串。 它需要一个分隔符和至少两个参数；否则将引发错误。 所有参数都隐式转换为字符串类型，然后连接在一起。 

隐式转换为字符串的过程遵循现有的数据类型转换规则。 有关行为和数据类型转换的详细信息，请参阅 [CONCAT (Transact SQL)](../../t-sql/functions/concat-transact-sql.md)。

### <a name="treatment-of-null-values"></a>NULL 值处理方式

`CONCAT_WS` 忽略 `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}` 设置。

如果所有参数都为 Null，则返回 `varchar(1)` 类型的空字符串。 

连接过程中会忽略 Null 值，并且不会添加分隔符。 这简化了连接字符串的常见方案，这些字符串通常具有空白值，如第二个地址字段。 请参阅示例 B。

如果方案需要使用分隔符将 null 值包括其中，请参阅使用 `ISNULL` 函数的示例 C。

## <a name="examples"></a>示例   

### <a name="a--concatenating-values-with-separator"></a>A.  使用分隔符连接值
以下示例连接 sys.databases 表中的三列，并使用 `- ` 分隔这些值。   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1 - SIMPLE - NONE |
|2 - SIMPLE - NONE |
|3 - FULL - NONE |
|4 - SIMPLE - NONE |


### <a name="b--skipping-null-values"></a>B.  跳过 NULL 值
以下示例忽略参数列表中的 `NULL` 值。

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>C.  从表中生成 CSV 文件
以下示例使用逗号作为分隔符，并添加回车符以生成列分隔值格式。

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, recovery_model_desc, containment_desc), char(13)) AS DatabaseInfo
FROM sys.databases
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
DatabaseInfo
------------   
1,SIMPLE,NONE
2,SIMPLE,NONE
3,FULL,NONE 
4,SIMPLE,NONE 
```

CONCAT_WS 将忽略列中的 NULL 值。 如果某些列可以为 null，请使用 `ISNULL` 函数包装它并提供默认值，如下例所示：

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>另请参阅
 [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md)  
 [FORMATMESSAGE (Transact-SQL)](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME (Transact-SQL)](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE (Transact-SQL)](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE (Transact-SQL)](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG (Transact-SQL)](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE (Transact-SQL)](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF (Transact-SQL)](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE (Transact-SQL)](../../t-sql/functions/translate-transact-sql.md)  
 [字符串函数 (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  

