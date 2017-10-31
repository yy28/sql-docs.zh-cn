---
title: "@@DBTS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 4a90150c55cdeb89788fdb86faf8aef8a1efdcd2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40dbts-transact-sql"></a>& #x 40; & #x 40; DBTS (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回当前数据库的当前 **timestamp** 数据类型的值。 此时间戳在数据库中保证是唯一的。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```
@@DBTS  
```  
  
## <a name="return-types"></a>返回类型
**varbinary**
  
## <a name="remarks"></a>注释  
@@DBTS返回当前数据库的最近使用的时间戳值。 插入或更新包含 **timestamp** 列的行时，将产生一个新的时间戳值。
  
@@DBTS函数不受事务隔离级别中的更改。
  
## <a name="examples"></a>示例  
下面的示例返回当前**时间戳**从[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]数据库。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@DBTS;  
```  
  
## <a name="see-also"></a>另请参阅
[配置函数 &#40;Transact SQL &#41;](../../t-sql/functions/configuration-functions-transact-sql.md)  
[光标并发 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/properties/cursor-concurrency-odbc.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40;Transact SQL &#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)
  
  

