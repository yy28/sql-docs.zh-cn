---
title: DAY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0f1d58e89e6fd7cdc4d8af85d3d8745e1bc15fa7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68119064"
---
# <a name="day-transact-sql"></a>DAY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

此函数返回表示指定 date 的日期（某月的一天）的整数  。
  
有关所有 [ 日期和时间数据类型及函数的概述，请参阅](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)日期和时间数据类型及函数 (Transact-SQL)[!INCLUDE[tsql](../../includes/tsql-md.md)]。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>参数  
*date*  
解析为下列某种数据类型的表达式：

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

对于 date， *接受列表达式、表达式、字符串文本或用户定义的变量*`DAY`。
  
## <a name="return-type"></a>返回类型  
**int**
  
## <a name="return-value"></a>返回值  
DAY 与 [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (day, date) 返回相同的值   。
  
如果 date 只包含时间部分，则  *将返回 1，即基准日*`DAY`。
  
## <a name="examples"></a>示例  
此语句返回 `30`，即天数本身。
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
此语句返回 `1900, 1, 1`。 date 参数具有数值  `0`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将 `0` 解释为 1900 年 1 月 1 日。
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


