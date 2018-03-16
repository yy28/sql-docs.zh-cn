---
title: DAY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
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
- DAY_TSQL
- DAY
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], DAY
- dates [SQL Server], functions
- DAY function [SQL Server]
- dates [SQL Server], days
- functions [SQL Server], date and time
- dateparts [SQL Server], day
ms.assetid: 2f4410ea-fd3e-4d69-ac4b-3b0091a084bc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 444df60a2cfe3adae045020b3db8d673946dccb1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="day-transact-sql"></a>DAY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回一个整数，该整数表示指定 date 的当天（某月的某一天）。
  
有关所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和时间数据类型及函数的概述，请参阅[日期和时间数据类型及函数 (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>参数  
*date*  
一个表达式，它可以解析为 time、date、smalldatetime、datetime、datetime2 或 datetimeoffset 值。 date 参数可以是表达式、列表达式、用户定义变量或字符串文字。
  
## <a name="return-type"></a>返回类型  
**int**
  
## <a name="return-value"></a>返回值  
DAY 与 [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (day, date) 返回相同的值。
  
如果 date 只包含时间部分，则返回值为 1，即基准日。
  
## <a name="examples"></a>示例  
下面的语句将返回 `30`。 这表示日期。
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
下面的语句将返回 `1900, 1, 1`。 date 的参数为数字 `0`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将 `0` 解释为 1900 年 1 月 1 日。
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


