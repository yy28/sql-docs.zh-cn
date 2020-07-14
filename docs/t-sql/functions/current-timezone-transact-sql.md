---
title: CURRENT_TIMEZONE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/28/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CURRENT_TIMEZONE
- CURRENT_TIMEZONE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- current time zone [SQL Server]
- current timezone [SQL Server]
- system time zone [SQL Server]
- system timezone [SQL Server]
- functions [SQL Server], time zone
- functions [SQL Server], timezone
- timezone [SQL Server], functions
- time zone [SQL Server], functions
- CURRENT_TIMEZONE function [SQL Server]
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 760da1491a7fbf4633cb02fe1fea8568e7ab9fa1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85684491"
---
# <a name="current_timezone-transact-sql"></a>CURRENT_TIMEZONE (Transact-SQL)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

此函数返回由服务器或实例观察到的时区的名称。 对于 SQL 数据库托管实例，返回值是根据实例创建期间分配的实例本身的时区返回，而不是根据基础操作系统的时区返回。
  
> [!NOTE]  
> 对于单一 SQL 数据库和共用 SQL 数据库，时区始终设置为 UTC，并且 `CURRENT_TIMEZONE` 返回 UTC 时区的名称。
  
## <a name="syntax"></a>语法  
  
```sql
CURRENT_TIMEZONE ( )  
```
  
## <a name="arguments"></a>参数

此函数没有参数。
  
## <a name="return-type"></a>返回类型  

**varchar**
  
## <a name="remarks"></a>备注  

`CURRENT_TIMEZONE` 是非确定性函数。 引用该列的视图和表达式无法进行索引。
  
## <a name="example"></a>示例

请注意，返回值反映服务器或实例的实际时区和语言设置。

```sql
SELECT CURRENT_TIMEZONE();  
/* Returned:  
(UTC+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna 
*/
```  
  
## <a name="see-also"></a>另请参阅

[SQL 数据库托管实例时区](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-timezone)

[CURRENT_TIMEZONE_ID()](https://docs.microsoft.com/sql/t-sql/functions/current-timezone-id-transact-sql)
