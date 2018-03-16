---
title: DATETIMEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
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
- DATETIMEFROMPARTS_TSQL
- DATETIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEFROMPARTS function
ms.assetid: 6008148b-bf75-4c98-9392-68a89fa0711c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ef125163e41d9ab1b2b465a31694428d22407501
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="datetimefromparts-transact-sql"></a>DATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

为指定的日期和时间返回 datetime 值。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATETIMEFROMPARTS ( year, month, day, hour, minute, seconds, milliseconds )  
```  
  
## <a name="arguments"></a>参数  
year  
用于指定年度的整数表达式。
  
month  
用于指定月份的整数表达式。
  
day  
用于指定日期的整数表达式。
  
hour  
用于指定小时的整数表达式。
  
minute  
用于指定分钟的整数表达式。
  
*seconds*  
用于指定秒的整数表达式。
  
milliseconds  
用于指定毫秒的整数表达式。
  
## <a name="return-types"></a>返回类型
**datetime**
  
## <a name="remarks"></a>Remarks  
DATETIMEFROMPARTS 返回完全初始化的 datetime 值。 如果参数无效，则引发错误。 如果所需的参数为 null，则返回 null。
  
此函数可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服务器以及更高版本上远程执行。 但在低于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的服务器版本中无法远程执行。
  
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
  
## <a name="see-also"></a>另请参阅
[datetime (Transact-SQL)](../../t-sql/data-types/datetime-transact-sql.md)
  
  

