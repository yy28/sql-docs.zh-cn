---
title: '@@DBTS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@DBTS_TSQL'
- '@@DBTS'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@DBTS function'
- timestamp data type
ms.assetid: 91842ddd-91c0-4445-a03f-116f6bc991d0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f9fca5c54451d13a8496d20e453d0bd89bf27fed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65945624"
---
# <a name="x40x40dbts-transact-sql"></a>&#x40;&#x40;DBTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此函数返回当前数据库的当前 timestamp 数据类型的值  。 当前数据库将具有确保唯一的时间戳值。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```
@@DBTS  
```  
  
## <a name="return-types"></a>返回类型
**varbinary**
  
## <a name="remarks"></a>Remarks  
@@DBTS 返回当前数据库最后使用的时间戳值。 插入或更新包含 timestamp 列的行时，会产生一个新的时间戳值  。
  
事务隔离级别的更改不会影响 @@DBTS 函数。
  
## <a name="examples"></a>示例  
此示例从 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库返回当前的 timestamp  。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@DBTS;  
```  
  
## <a name="see-also"></a>另请参阅
[配置函数 (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)  
[游标并发 (ODBC)](../../relational-databases/native-client-odbc-cursors/properties/cursor-concurrency-odbc.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION (Transact-SQL)](../../t-sql/functions/min-active-rowversion-transact-sql.md)
  
  
