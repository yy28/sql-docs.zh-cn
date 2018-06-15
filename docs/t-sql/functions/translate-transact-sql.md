---
title: TRANSLATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords:
- TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 4e070109028ed446636610b1008b76fc33bf495e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33058875"
---
# <a name="translate-transact-sql"></a>TRANSLATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

在第二个参数中指定的某些字符转换为字符目标集后，返回作为第一个参数提供的字符串。

## <a name="syntax"></a>语法   
```
TRANSLATE ( inputString, characters, translations) 
```

## <a name="arguments"></a>参数   

inputString   
任何字符类型（nvarchar、varchar、nchar、char）的[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。

字符   
任何包含应替换字符的字符类型的[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。

翻译   
类型和长度与第二个参数匹配的字符[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。

## <a name="return-types"></a>返回类型   
返回与 `inputString`（第二个参数中的字符被替换为第三个参数中的匹配字符）具有相同类型的字符表达式。

## <a name="remarks"></a>Remarks   

如果字符和转换长度不同，则 `TRANSLATE` 函数将返回错误。 如果 null 值作为字符或替换参数提供，则 `TRANSLATE` 函数应返回不变的输入。 `TRANSLATE` 函数的行为应与 [REPLACE](../../t-sql/functions/replace-transact-sql.md) 函数的行为相同。   

`TRANSLATE` 函数行为等同于使用多个 `REPLACE` 函数。

`TRANSLATE` 始终可以感知 SC 排序规则。

## <a name="examples"></a>示例   

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>A. 将方括号和大括号替换为圆括号    
以下查询将输入字符串中的方括号和大括号替换为圆括号：
```
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
2*(3+4)/(7-2)
```

>  [!NOTE]
>  此示例中的 `TRANSLATE` 函数相当于以下语句使用`REPLACE`：`SELECT REPLACE(REPLACE(REPLACE(REPLACE('2*[3+4]/{7-2}','[','('), ']', ')'), '{', '('), '}', ')');`，但是更加的简单 


###  <a name="b-convert-geojson-points-into-wkt"></a>B. 将 GeoJSON 点转换为 WKT    
GeoJSON 格式可用于对各种地理数据结构进行编码。 通过 `TRANSLATE` 函数，开发人员可以轻松地将 GeoJSON 点转换为 WKT 格式，反之亦然。 以下查询将输入中的方括号和大括号替换为圆括号：   
```sql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   


|点  |坐标 |  
---------|--------- |
(137.4  72.3) |[137.4,72.3] |


## <a name="see-also"></a>另请参阅
 [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS (Transact-SQL)](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE (Transact-SQL)](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME (Transact-SQL)](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE (Transact-SQL)](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE (Transact-SQL)](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG (Transact-SQL)](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE (Transact-SQL)](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF (Transact-SQL)](../../t-sql/functions/stuff-transact-sql.md)  
 [字符串函数 (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   

