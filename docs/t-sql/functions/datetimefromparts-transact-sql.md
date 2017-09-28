---
title: "DATETIMEFROMPARTS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATETIMEFROMPARTS_TSQL
- DATETIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEFROMPARTS function
ms.assetid: 6008148b-bf75-4c98-9392-68a89fa0711c
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 79bddc120ba326e625525098bbe58cf098795108
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="datetimefromparts-transact-sql"></a>DATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

返回**datetime**值的指定的日期和时间。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATETIMEFROMPARTS ( year, month, day, hour, minute, seconds, milliseconds )  
```  
  
## <a name="arguments"></a>参数  
*年*  
用于指定年度的整数表达式。
  
*月*  
用于指定月份的整数表达式。
  
*一天*  
用于指定日期的整数表达式。
  
*小时*  
用于指定小时的整数表达式。
  
*分钟*  
用于指定分钟的整数表达式。
  
*seconds*  
用于指定秒的整数表达式。
  
*毫秒*  
用于指定毫秒的整数表达式。
  
## <a name="return-types"></a>返回类型
**datetime**
  
## <a name="remarks"></a>注释  
**DATETIMEFROMPARTS**返回完全初始化**datetime**值。 如果自变量无效，则引发错误。 如果需要自变量为 null，则返回 null。
  
此函数可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服务器以及更高版本上远程执行。 它将不到具有以下版本的服务器进行远程处理[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
  
## <a name="examples"></a>示例  
  
```sql
SELECT DATETIMEFROMPARTS ( 2010, 12, 31, 23, 59, 59, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.000  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT DATETIMEFROMPARTS ( 2010, 12, 31, 23, 59, 59, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[datetime &#40;Transact SQL &#41;](../../t-sql/data-types/datetime-transact-sql.md)
  
  


