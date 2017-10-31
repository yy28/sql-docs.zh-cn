---
title: "STRING_SPLIT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRING_SPLIT
- STRING_SPLIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_SPLIT function
ms.assetid: 3273dbf3-0b4f-41e1-b97e-b4f67ad370b9
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 049bdf1021d57e28ed94e11c89aa997ee0eba5e5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  将拆分使用指定的分隔符的字符表达式。  
  
> [!NOTE]  
>  **STRING_SPLIT**函数是仅在兼容性级别 130 下可用。 如果你的数据库兼容性级别低于 130，SQL Server 将不能以查找并执行**STRING_SPLIT**函数。 你可以使用以下命令更改数据库的兼容级别：  
> ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
>   
>  请注意，兼容性级别 120 可能甚至在新的 Azure SQL 数据库中的默认值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
STRING_SPLIT ( string , separator )  
```  
  
## <a name="arguments"></a>参数  
 *string*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何字符类型 (即**nvarchar**， **varchar**， **nchar**或**char**)。  
  
 *分隔符*  
 是单个字符[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何字符类型 (例如**nvarchar(1)**， **varchar(1)**， **nchar(1)**或**char （1)**) 用作分隔符的串联字符串。  
  
## <a name="return-types"></a>返回类型  
 返回包含片段的单列的表。 列的名称是**值**。 返回**nvarchar**如果任何输入参数都是**nvarchar**或**nchar**。 否则返回**varchar**。 返回类型的长度是与字符串自变量的长度相同。  
  
## <a name="remarks"></a>注释  
 **STRING_SPLIT**采用应该被划分的字符串和将用于将字符串划分的分隔符。 它将返回具有子字符串的单列的表。 例如，以下语句`SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');`使用空格字符作为分隔符，返回以下结果表：  
  
|值|  
|-----------|  
|Lorem|  
|ipsum|  
|dolor|  
|位于以下位置：|  
|amet。|  
  
 如果输入的字符串是**NULL**、 **STRING_SPLIT**表值函数返回一个空表。  
  
 **STRING_SPLIT**至少需要兼容性模式 130。  
  
## <a name="examples"></a>示例  
  
### <a name="a-split-comma-separated-value-string"></a>A. 拆分以逗号分隔的值字符串  
 分析的值以逗号分隔列表，并返回所有非空令牌：  
  
```  
  
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';  
  
```  
  
 如果分隔符之间没有任何内容，STRING_SPLIT 将返回空字符串。 条件 RTRIM(value) <> ' 将移除空标记。  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>B. 拆分以逗号分隔的列中的值字符串  
 Product 表具有一个列的以下示例所示的标记的逗号单独列表：  
  
|ProductId|Name|Tags|  
|---------------|----------|----------|  
|1|完整手指手套|服装，道路，touring bike|  
|2|LL 耳机|自行车|  
|3|HL Mountain Frame|自行车 mountain|  
  
 下面的查询转换的标记的每个列表，并将它们与原始行联接起来：  
  
```  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|ProductId|Name|值|  
|---------------|----------|-----------|  
|1|完整手指手套|服装|  
|1|完整手指手套|road|  
|1|完整手指手套|touring|  
|1|完整手指手套|自行车|  
|2|LL 耳机|自行车|  
|3|HL Mountain Frame|自行车|  
|3|HL Mountain Frame|mountain|  
  
### <a name="c-aggregation-by-values"></a>C. 值的聚合  
 用户必须创建一个报表来显示每个产品，并筛选仅与 2 个以上的产品的标记数按排序每个标记的产品数。  
  
```  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```  
  
### <a name="d-search-by-tag-value"></a>D. 按标记值搜索  
 开发人员必须创建按关键字查找文章的查询。 它们可以使用以下查询：  
  
 若要查找的产品与单个标记 （服装）：  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```  
  
 查找与这两个指定的标记 （服装和道路） 的产品：  
  
```  
  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road');  
```  
  
### <a name="e-find-rows-by-list-of-values"></a>E. 查找行的值列表  
 开发人员必须创建一个查询，查找文章的 id 的列表。 它们可以使用以下查询：  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')   
    ON value = ProductId;  
```  
  
 这是常见的防模式，如在应用程序层中创建的动态 SQL 字符串的替换或[!INCLUDE[tsql](../../includes/tsql-md.md)]，或通过使用 LIKE 运算符：  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```  
  
## <a name="see-also"></a>另请参阅  
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [子字符串 &#40;Transact SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
  
  

