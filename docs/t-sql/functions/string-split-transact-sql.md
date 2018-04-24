---
title: STRING_SPLIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5204f8df5f2267421c27528ef85126e118fe56b5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  使用指定的分隔符拆分字符表达式。  
  
> [!NOTE]  
>  STRING_SPLIT 函数仅在兼容级别 130 下可用。 如果数据库兼容级别低于 130，SQL Server 将无法找到和执行 STRING_SPLIT 函数。 你可以使用以下命令更改数据库的兼容级别：  
> ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
>   
>  请注意，兼容级别 120 可能是默认级别，即使在新的 Azure SQL 数据库中也是如此。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
STRING_SPLIT ( string , separator )  
```  
  
## <a name="arguments"></a>参数  
 *string*  
 任何字符类型（即 nvarchar、varchar、nchar 或 char）的[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 separator  
 任何字符类型（即 nvarchar(1)、varchar(1)、nchar(1) 或 char(1)）的单字符[表达式](../../t-sql/language-elements/expressions-transact-sql.md)，用作串联字符串的分隔符。  
  
## <a name="return-types"></a>返回类型  
 返回包含片段的单列表。 该列名为“value”。 如果任何输入参数为 nvarchar 或 nchar，则返回 nvarchar。 否则，返回 varchar。 返回类型的长度与字符串参数的长度相同。  
  
## <a name="remarks"></a>Remarks  
 STRING_SPLIT 采用应被拆分的字符串和将用于拆分字符串的分隔符。 返回包含子字符串的单列表。 例如，以下语句 `SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');` 使用空格字符作为分隔符，返回以下的结果表：  
  
|值|  
|-----------|  
|Lorem|  
|ipsum|  
|dolor|  
|sit|  
|amet.|  
  
 如果输入字符串为 NULL，则 STRING_SPLIT 表值函数返回一个空表。  
  
 STRING_SPLIT 至少要求使用兼容模式 130。  
  
## <a name="examples"></a>示例  
  
### <a name="a-split-comma-separated-value-string"></a>A. 拆分逗号分隔值字符串  
 分析逗号分隔值列表，并返回所有非空标记：  
  
```  
  
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';  
  
```  
  
 如果分隔符之间没有任何内容，STRING_SPLIT 将返回空字符串。 条件 RTRIM(value) <> '' 将删除空标记。  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>B. 拆分一列中的逗号分隔值字符串  
 生产表中的某一列为逗号分隔的标记列表，如以下示例所示：  
  
|ProductId|“属性”|Tags|  
|---------------|----------|----------|  
|@shouldalert|Full-Finger Gloves|clothing,road,touring,bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike,mountain|  
  
 下面的查询转换每个标记列表，并将它们与原始行联接起来：  
  
```  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|ProductId|“属性”|值|  
|---------------|----------|-----------|  
|@shouldalert|Full-Finger Gloves|clothing|  
|@shouldalert|Full-Finger Gloves|road|  
|@shouldalert|Full-Finger Gloves|touring|  
|@shouldalert|Full-Finger Gloves|bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike|  
|3|HL Mountain Frame|mountain|  
  
### <a name="c-aggregation-by-values"></a>C. 按值聚合  
 用户必须创建一个报表，表中显示每个标记的产品数量并按产品数量排序，然后只筛选出产品数量在 2 个以上的标记。  
  
```  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```  
  
### <a name="d-search-by-tag-value"></a>D. 按标记值搜索  
 开发人员必须创建按关键字查找文章的查询。 可以使用以下查询：  
  
 查找具有单个标记 (clothing) 的产品：  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```  
  
 查找具有两个指定标记（clothing 和 road）的产品：  
  
```  
  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road');  
```  
  
### <a name="e-find-rows-by-list-of-values"></a>E. 按一系列值查找行  
 开发人员必须创建一个按 ID 列表查找文章的查询。 可以使用以下查询：  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')   
    ON value = ProductId;  
```  
  
 以下是常见反模式（例如在应用程序层或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中创建动态 SQL ，或使用 LIKE 运算符）的替代方式：  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```  
  
## <a name="see-also"></a>另请参阅  
 [LEFT (Transact-SQL)](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM (Transact-SQL)](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT (Transact-SQL)](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM (Transact-SQL)](../../t-sql/functions/rtrim-transact-sql.md)  
 [SUBSTRING (Transact-SQL)](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM (Transact-SQL)](../../t-sql/functions/trim-transact-sql.md)  
 [字符串函数 (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
