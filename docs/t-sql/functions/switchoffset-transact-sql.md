---
title: "SWITCHOFFSET (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/02/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SWITCHTZ
- SWITCHTZ_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- functions [SQL Server], time
- functions [SQL Server], date and time
- SWITCHOFFSET function [SQL Server]
- time [SQL Server], functions
- date and time [SQL Server], SWITCHOFFSET
- time zones [SQL Server]
ms.assetid: 32a48e36-0aa4-4260-9fe9-cae9197d16c5
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 712b6c1b582c2eec76958eafaad5d02f2e411640
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="switchoffset-transact-sql"></a>SWITCHOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回**datetimeoffset**从存储的时区偏移量更改为指定的新时区偏移量的值。  
  
 有关的所有概述[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和时间数据类型和函数，请参阅[日期和时间数据类型和函数 &#40;Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SWITCHOFFSET ( DATETIMEOFFSET, time_zone )   
```  
  
## <a name="arguments"></a>参数  
 *DATETIMEOFFSET*  
 是可被解析为一个表达式**datetimeoffset(n)**值。  
  
 *time_zone*  
 是一个格式为 [+|-]TZH:TZM 的字符串，或是一个表示时区偏移量的带符号的整数（分钟数），假定它能够感知夏时制并作出相应的调整。  
  
## <a name="return-type"></a>返回类型  
 **datetimeoffset**使用的小数部分精度*DATETIMEOFFSET*自变量。  
  
## <a name="remarks"></a>注释  
 使用 SWITCHOFFSET 选择**datetimeoffset**值转换为不同于最初存储的时区偏移量的时区偏移量。 SWITCHOFFSET 不会更新存储*time_zone*值。  
  
 SWITCHOFFSET 可以用于更新**datetimeoffset**列。  
  
 将 SWITCHOFFSET 用于函数 GETDATE() 可能导致查询运行缓慢。 这是因为查询优化器无法获取 datetime 值的准确基数估计值。 要解决此问题，请使用 OPTION (RECOMPILE) 查询提示以强制查询优化器在下次执行同一查询时重新编译查询计划。 优化器将得到准确的基数估计值并生成更高效的查询计划。 有关 RECOMPILE 查询提示的详细信息，请参阅[查询提示 &#40;Transact SQL &#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
```  
DECLARE @dt datetimeoffset = switchoffset (CONVERT(datetimeoffset, GETDATE()), '-04:00');   
SELECT * FROM t    
WHERE c1 > @dt OPTION (RECOMPILE);  
  
```  
  
## <a name="examples"></a>示例  
 下例使用 `SWITCHOFFSET` 显示与数据库中所存储的值不同的时区偏移量。  
  
```  
CREATE TABLE dbo.test   
    (  
    ColDatetimeoffset datetimeoffset  
    );  
GO  
INSERT INTO dbo.test   
VALUES ('1998-09-20 7:45:50.71345 -5:00');  
GO  
SELECT SWITCHOFFSET (ColDatetimeoffset, '-08:00')   
FROM dbo.test;  
GO  
--Returns: 1998-09-20 04:45:50.7134500 -08:00  
SELECT ColDatetimeoffset  
FROM dbo.test;  
--Returns: 1998-09-20 07:45:50.7134500 -05:00  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下例使用 `SWITCHOFFSET` 显示与数据库中所存储的值不同的时区偏移量。  
  
```  
CREATE TABLE dbo.test   
    (  
    ColDatetimeoffset datetimeoffset  
    );  
GO  
INSERT INTO dbo.test   
VALUES ('1998-09-20 7:45:50.71345 -5:00');  
GO  
SELECT SWITCHOFFSET (ColDatetimeoffset, '-08:00')   
FROM dbo.test;  
GO  
--Returns: 1998-09-20 04:45:50.7134500 -08:00  
SELECT ColDatetimeoffset  
FROM dbo.test;  
--Returns: 1998-09-20 07:45:50.7134500 -05:00  
```  
  
## <a name="see-also"></a>另请参阅  
 [强制转换和转换 &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [时区 &AMP; #40;Transact SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  



