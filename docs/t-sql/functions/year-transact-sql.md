---
title: "年 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- YEAR
- YEAR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server], years
- date and time [SQL Server], YEAR
- functions [SQL Server], date and time
- YEAR function [SQL Server]
- dateparts [SQL Server], year
ms.assetid: 74aa7ccc-8575-4018-80cf-14aeca379687
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ee3f419d092f6e8b327dd5e4ac498afa4036ebbb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="year-transact-sql"></a>YEAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回一个整数，表示指定的年份*日期*。  
  
 有关的所有概述[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和时间数据类型和函数，请参阅[日期和时间数据类型和函数 &#40;Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
YEAR ( date )  
```  
  
## <a name="arguments"></a>参数  
 *date*  
 是可被解析为一个表达式**时间**，**日期**， **smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。 *日期*参数可以是表达式、 列表达式、 用户定义变量或字符串文本。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="return-value"></a>返回值  
 相同的值，则 YEAR 返回[DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**年**，*日期*)。  
  
 如果*日期*仅包含时间部分，则返回值是 1900 年基的年份。  
  
## <a name="examples"></a>示例  
 下面的语句将返回 `2007`。 它是表示年份的数字。  
  
```  
SELECT YEAR('2007-04-30T01:01:01.1234567-07:00');  
```  
  
 下面的语句将返回 `1900, 1, 1`。 自变量*日期*是数`0`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将 `0` 解释为 1900 年 1 月 1 日。  
  
```  
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的语句将返回 `2010`。 它是表示年份的数字。  
  
```  
SELECT YEAR('2010-07-20T01:01:01.1234');  
```  
  
 下面的语句将返回 `1900, 1, 1`。 自变量*日期*是数`0`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将 `0` 解释为 1900 年 1 月 1 日。  
  
```  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>另请参阅  
 [CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  


