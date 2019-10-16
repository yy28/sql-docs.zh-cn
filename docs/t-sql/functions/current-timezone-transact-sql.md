---
title: CURRENT_TIMEZONE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
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
ms.openlocfilehash: e659ae78b81cb6888e749bd40546efe16b4c542d
ms.sourcegitcommit: aece9f7db367098fcc0c508209ba243e05547fe1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2019
ms.locfileid: "72261326"
---
# <a name="current_timezone-transact-sql"></a>CURRENT_TIMEZONE (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>Remarks  

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
