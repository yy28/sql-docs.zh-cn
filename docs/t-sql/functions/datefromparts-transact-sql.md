---
title: DATEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATEFROMPARTS_TSQL
- DATEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATEFROMPARTS function
ms.assetid: 5b885376-87aa-41f1-9e18-04987aead250
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0b5348706b7326a56b5d1367104301db557b8cd8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="datefromparts-transact-sql"></a>DATEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

返回表示指定年、月、日的 date 值。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATEFROMPARTS ( year, month, day )  
```  
  
## <a name="arguments"></a>参数  
year  
用于指定年度的整数表达式。
  
month  
指定月份（从 1 到 12）的整数表达式。
  
day  
用于指定日期的整数表达式。
  
## <a name="return-types"></a>返回类型
**date**
  
## <a name="remarks"></a>Remarks  
DATEFROMPARTS 返回一个 date 值，日期部分设置为指定的年、月和日，而时间部分设置为默认值。 如果参数无效，则引发错误。 如果所需的参数为 null，则返回 null。
  
此函数可以在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 服务器以及更高版本上远程执行。 但在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 之下的服务器版本中无法远程执行。
  
## <a name="examples"></a>示例  
以下示例说明了 DATEFROMPARTS 函数的用法。
  
```sql
SELECT DATEFROMPARTS ( 2010, 12, 31 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------  
2010-12-31  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[date (Transact-SQL)](../../t-sql/data-types/date-transact-sql.md)
  
  

