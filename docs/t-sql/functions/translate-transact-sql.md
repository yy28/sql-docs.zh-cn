---
title: "翻译 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords:
- TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 583c414206a0acc79d1abdfff34728c38711a855
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="translate-transact-sql"></a>翻译 (Transact SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

返回后在第二个参数中指定某些字符转换为目标的一组字符作为第一个参数提供的字符串。

## <a name="syntax"></a>语法   
```
TRANSLATE ( inputString, characters, translations) 
```

## <a name="arguments"></a>参数   

inputString   
是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何字符类型 （nvarchar、 varchar、 nchar、 char）。

字符   
是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何字符类型且包含应替换的字符。

翻译   
是字符[表达式](../../t-sql/language-elements/expressions-transact-sql.md)匹配第二个自变量类型和长度。

## <a name="return-types"></a>返回类型   
返回与相同的类型的字符表达式`inputString`其中将从第二个参数的字符替换为从第三个自变量匹配的字符。

## <a name="remarks"></a>注释   

`TRANSLATE`如果字符和翻译具有不同长度，则函数将返回错误。 `TRANSLATE`如果作为字符或替换自变量提供 null 值，函数应返回不变的输入。 行为`TRANSLATE`函数应等于[替换](../../t-sql/functions/replace-transact-sql.md)函数。   

行为`TRANSLATE`函数等同于使用多个`REPLACE`函数。

`TRANSLATE`始终是 SC 排序规则感知的。

## <a name="examples"></a>示例   

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>A. 将替换为正则大括号方形和大括号    
以下查询使用括号替换输入字符串中的正方形和大括号：
```
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
2*(3+4)/(7-2)
```

>  [!NOTE]
>  `TRANSLATE`在此示例中的函数是等效于但比以下语句使用变得更加简单`REPLACE`:`SELECT REPLACE(REPLACE(REPLACE(REPLACE('2*[3+4]/{7-2}','[','('), ']', ')'), '{', '('), '}', ')');` 


###  <a name="b-convert-geojson-points-into-wkt"></a>B. 将 GeoJSON 点转换为 WKT    
GeoJSON 是一种格式进行编码各种地理数据结构。 与`TRANSLATE`函数，开发人员可以轻松地将转换 GeoJSON 点为 WKT 格式，反之亦然。 下面的查询替换正则大括号中输入的正方形和大括号：   
```tsql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   


|点  |坐标 |  
---------|--------- |
(137.4  72.3) |[137.4,72.3] |


## <a name="see-also"></a>另请参阅

[字符串函数 (TRANSACT-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   
[REPLACE (Transact SQL)](../../t-sql/functions/replace-transact-sql.md)   


