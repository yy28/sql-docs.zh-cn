---
title: DATETIMEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: ff10c9dff219c3610938f5944fd054b535226afe
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39458001"
---
# <a name="datetimefromparts-transact-sql"></a>DATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

此函数对指定日期和时间参数返回 datetime 值。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATETIMEFROMPARTS ( year, month, day, hour, minute, seconds, milliseconds )  
```  
  
## <a name="arguments"></a>参数  
year  
指定年份的整数表达式。
  
month  
指定月份的整数表达式。
  
day  
指定日期的整数表达式。
  
hour  
指定小时的整数表达式。
  
minute  
指定分钟的整数表达式。
  
*seconds*  
指定秒数的整数表达式。
  
milliseconds  
指定毫秒数的整数表达式。
  
## <a name="return-types"></a>返回类型
**datetime**
  
## <a name="remarks"></a>Remarks  
`DATETIMEFROMPARTS` 返回完全初始化的 datetime 值。 如果至少有一个必需参数具有无效值，`DATETIMEFROMPARTS` 将引发错误。 如果至少有一个必需参数具有 NULL 值，则 `DATETIMEFROMPARTS` 返回 NULL。
  
此函数支持在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 及更高版本的服务器上远程执行。 但不支持在版本低于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的服务器上远程执行。
  
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
  
  

