---
title: "CONCAT_WS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CONCAT_WS
- CONCAT_WS_TSQL
dev_langs: TSQL
helpviewer_keywords: CONCAT_WS function
ms.assetid: f1375fd7-a2fd-48bf-922a-4f778f0deb1f
caps.latest.revision: "5"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7d7932c1887c82b2a10702f9054706e4cf9bce71
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

在第 1 个参数中指定的分隔符与连接数目可变的参数。 (`CONCAT_WS`指示*使用分隔符连接*。)

##  <a name="syntax"></a>语法   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>参数   
separator  
是任何字符类型的表达式 (`nvarchar`， `varchar`， `nchar`，或`char`)。

argument1，argument2，参数*N*  
是任何类型的表达式。

## <a name="return-types"></a>返回类型
字符串。 长度和类型取决于输入。

## <a name="remarks"></a>注释   
`CONCAT_WS`采用数量可变的自变量并将它们连接到单个字符串的第一个参数用作分隔符。 它需要分隔符，至少为两个自变量;否则，将引发错误。 所有参数隐式转换为字符串类型，然后串联在一起。 

隐式转换为字符串的过程遵循现有的数据类型转换规则。 有关行为和数据类型转换的详细信息，请参阅[CONCAT (Transact SQL)](../../t-sql/functions/concat-transact-sql.md)。

### <a name="treatment-of-null-values"></a>NULL 值处理

`CONCAT_WS`将忽略`SET CONCAT_NULL_YIELDS_NULL {ON|OFF}`设置。

如果所有的自变量是 null，类型的空字符串`varchar(1)`返回。 

Null 值在连接，过程中忽略，并且不会添加分隔符。 这简化了常见的方案的串联字符串通常具有空白值，如第二个地址字段。 请参阅示例 b。

如果你的方案需要 null 值将包括分隔符，请参阅示例 C 使用`ISNULL`函数。

## <a name="examples"></a>示例   

### <a name="a--concatenating-values-with-separator"></a>A.  带分隔符串联值
下面的示例连接从 sys.databases 表格中，分隔各个值与三列`- `。   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1-简单-无 |
|2-简单-无 |
|3-完全-无 |
|4-简单-无 |


### <a name="b--skipping-null-values"></a>B.  正在跳过的 NULL 值
下面的示例将忽略`NULL`自变量列表中的值。

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
下面的示例中使用逗号作为分隔符，并添加回车符导致列分隔的值格式。

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

CONCAT_WS 将忽略列中的 NULL 值。 某些列是否可以为 null，则将其与包装`ISNULL`函数并提供类似下面的示例中的默认值：

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>另请参阅
 [CONCAT &#40;Transact SQL &#41;](../../t-sql/functions/concat-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact SQL &#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  

