---
title: "CURRENT_TIMESTAMP (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURRENT_TIMESTAMP
- CURRENT_TIMESTAMP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- niladic functions
- current date and time [SQL Server]
- time [SQL Server], current
- date and time [SQL Server], CURRENT_TIMESTAMP
- functions [SQL Server], time
- system date and time [SQL Server]
- system time [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], current date and time
- dates [SQL Server], system date and time
- CURRENT_TIMESTAMP function [SQL Server]
- time [SQL Server], system
ms.assetid: c724d9cc-7b1f-4c71-bdf5-08bc52b33afc
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0a9896ac36bbcfa34cb2697634445dcc2a77cfa2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="currenttimestamp-transact-sql"></a>CURRENT_TIMESTAMP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回为当前数据库系统时间戳**datetime**而无需数据库时区偏移量的值。 此值得自运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机的操作系统。
  
> [!NOTE]  
>  SYSDATETIME 和 SYSUTCDATE 在秒的小数部分精度上要比 GETDATE 和 GETUTCDATE 高。 SYSDATETIMEOFFSET 包含系统时区偏移量。 SYSDATETIME、SYSUTCDATE 和 SYSDATETIMEOFFSET 可分配给采用任意日期和时间类型的变量。  
  
此函数是 ANSI SQL 等效于[GETDATE](../../t-sql/functions/getdate-transact-sql.md)。
  
有关的所有概述[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和时间数据类型和函数，请参阅[日期和时间数据类型和函数](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
CURRENT_TIMESTAMP  
```  
  
## <a name="arguments"></a>参数  
无参数。
  
## <a name="return-type"></a>返回类型  
**datetime**
  
## <a name="remarks"></a>注释  
[!INCLUDE[tsql](../../includes/tsql-md.md)]语句可以指 CURRENT_TIMESTAMP 随处它们可引用**datetime**表达式。
  
CURRENT_TIMESTAMP 是非确定性函数。 引用该列的视图和表达式无法进行索引。
  
## <a name="examples"></a>示例  
下面的示例使用了六个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回当前日期和时间才能返回日期、 时间，或两者的系统函数。 这些值是连续返回的，因此，它们的秒小数部分可能有所不同。
  
### <a name="a-get-the-current-system-date-and-time"></a>A. 获取当前系统日期和时间  
  
```sql
SELECT SYSDATETIME()  
    ,SYSDATETIMEOFFSET()  
    ,SYSUTCDATETIME()  
    ,CURRENT_TIMESTAMP  
    ,GETDATE()  
    ,GETUTCDATE();  
/* Returned:  
SYSDATETIME()      2007-04-30 13:10:02.0474381  
SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00  
SYSUTCDATETIME()   2007-04-30 20:10:02.0474381  
CURRENT_TIMESTAMP  2007-04-30 13:10:02.047  
GETDATE()          2007-04-30 13:10:02.047  
GETUTCDATE()       2007-04-30 20:10:02.047  
```  
  
### <a name="b-get-the-current-system-date"></a>B. 获取当前系统日期  
  
```sql
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
  
/* Returned   
SYSDATETIME()      2007-05-03  
SYSDATETIMEOFFSET()2007-05-03  
SYSUTCDATETIME()   2007-05-04  
CURRENT_TIMESTAMP  2007-05-03  
GETDATE()          2007-05-03  
GETUTCDATE()       2007-05-04  
*/  
```  
  
### <a name="c-get-the-current-system-time"></a>C. 获取当前系统时间  
  
```sql
SELECT CONVERT (time, SYSDATETIME())  
    ,CONVERT (time, SYSDATETIMEOFFSET())  
    ,CONVERT (time, SYSUTCDATETIME())  
    ,CONVERT (time, CURRENT_TIMESTAMP)  
    ,CONVERT (time, GETDATE())  
    ,CONVERT (time, GETUTCDATE());  
  
/* Returned  
SYSDATETIME()      13:18:45.3490361  
SYSDATETIMEOFFSET()13:18:45.3490361  
SYSUTCDATETIME()   20:18:45.3490361  
CURRENT_TIMESTAMP  13:18:45.3470000  
GETDATE()          13:18:45.3470000  
GETUTCDATE()       20:18:45.3470000  
*/  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT CURRENT_TIMESTAMP;  
```  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


