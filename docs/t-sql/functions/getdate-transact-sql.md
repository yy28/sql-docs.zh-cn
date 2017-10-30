---
title: "GETDATE (Transact SQL) |Microsoft 文档"
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
- GETDATE_TSQL
- GETDATE
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- GETDATE function [SQL Server]
- current date and time [SQL Server]
- time [SQL Server], current
- functions [SQL Server], time
- system date and time [SQL Server]
- system time [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], current date and time
- date and time [SQL Server], GETDATE
- dates [SQL Server], system date and time
- time [SQL Server], system
ms.assetid: bebe3b65-2b3e-4c73-bf80-ff1132c680a7
caps.latest.revision: 46
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1c0cf660d5240e6a5222c44334f31f0beb94a749
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="getdate-transact-sql"></a>GETDATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回为当前数据库系统时间戳**datetime**而无需数据库时区偏移量的值。 此值得自运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机的操作系统。  
  
> [!NOTE]  
>  与 GETDATE 和 GETUTCDATE 比较而言，SYSDATETIME 和 SYSUTCDATETIME 的秒的小数部分精度更高。 SYSDATETIMEOFFSET 包含系统时区偏移量。 SYSDATETIME、SYSUTCDATETIME 和 SYSDATETIMEOFFSET 可以分配给采用任意日期和时间类型的变量。  
  
 有关的所有概述[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和时间数据类型和函数，请参阅[日期和时间数据类型和函数 &#40;Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
GETDATE ( )  
```  
  
## <a name="return-type"></a>返回类型  
 **datetime**  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]语句可以引用的 GETDATE 随处它们可引用**datetime**表达式。  
  
 GETDATE 是非确定性函数。 不能对在列中引用该函数的视图和表达式建立索引。  
  
 将 SWITCHOFFSET 用于函数 GETDATE() 可能导致查询运行缓慢，这是因为查询优化器无法获取 GETDATE 值的准确基数估计值。 我们建议您预先计算 GETDATE 值，然后在查询中指定该值，如以下示例中所示。 此外，使用选项 （重新编译） 中的查询提示强制查询优化器重新编译查询计划在下次执行相同的查询。 优化器然后具有 GETDATE() 的准确基数估值，将生成更高效的查询计划。  
  
```  
DECLARE @dt datetimeoffset = switchoffset (CONVERT(datetimeoffset, GETDATE()), '-04:00');   
SELECT * FROM t    
WHERE c1 > @dt OPTION (RECOMPILE);  
  
```  
  
## <a name="examples"></a>示例  
 以下示例使用六个返回当前日期和时间的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统函数来返回日期和/或时间。 序列; 中返回的值因此，其秒的小数部分可能会有所不同。  
  
### <a name="a-getting-the-current-system-date-and-time"></a>A. 获取当前系统日期和时间  
  
```  
SELECT SYSDATETIME()  
    ,SYSDATETIMEOFFSET()  
    ,SYSUTCDATETIME()  
    ,CURRENT_TIMESTAMP  
    ,GETDATE()  
    ,GETUTCDATE();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
SYSDATETIME()      2007-04-30 13:10:02.0474381
SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00
SYSUTCDATETIME()   2007-04-30 20:10:02.0474381
CURRENT_TIMESTAMP  2007-04-30 13:10:02.047
GETDATE()          2007-04-30 13:10:02.047
GETUTCDATE()       2007-04-30 20:10:02.047
```  
  
### <a name="b-getting-the-current-system-date"></a>B. 获取当前系统日期  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
SYSDATETIME()          2007-05-03  
SYSDATETIMEOFFSET()    2007-05-03  
SYSUTCDATETIME()       2007-05-04  
CURRENT_TIMESTAMP      2007-05-03  
GETDATE()              2007-05-03  
GETUTCDATE()           2007-05-04
``` 
  
### <a name="c-getting-the-current-system-time"></a>C. 获取当前系统时间  
  
```  
SELECT CONVERT (time, SYSDATETIME())  
    ,CONVERT (time, SYSDATETIMEOFFSET())  
    ,CONVERT (time, SYSUTCDATETIME())  
    ,CONVERT (time, CURRENT_TIMESTAMP)  
    ,CONVERT (time, GETDATE())  
    ,CONVERT (time, GETUTCDATE());  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
SYSDATETIME()      13:18:45.3490361  
SYSDATETIMEOFFSET()13:18:45.3490361  
SYSUTCDATETIME()   20:18:45.3490361  
CURRENT_TIMESTAMP  13:18:45.3470000  
GETDATE()          13:18:45.3470000  
GETUTCDATE()       20:18:45.3470000  
```
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例使用三个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系统函数，返回当前日期和时间返回日期、 时间或两者。 序列; 中返回的值因此，其秒的小数部分可能会有所不同。  
  
### <a name="d-getting-the-current-system-date-and-time"></a>D. 获取当前系统日期和时间  
  
```  
SELECT SYSDATETIME()  
    ,CURRENT_TIMESTAMP  
    ,GETDATE();  
```  
  
### <a name="e-getting-the-current-system-date"></a>E. 获取当前系统日期  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE());  
  
```  
  
### <a name="f-getting-the-current-system-time"></a>F. 获取当前系统时间  
  
```  
SELECT CONVERT (time, SYSDATETIME())  
    ,CONVERT (time, CURRENT_TIMESTAMP)  
    ,CONVERT (time, GETDATE());  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  


