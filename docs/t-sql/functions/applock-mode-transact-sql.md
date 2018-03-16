---
title: APPLOCK_MODE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- APPLOCK_MODE_TSQL
- APPLOCK_MODE
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- APPLOCK_MODE function
ms.assetid: e43d4917-77f1-45cc-b231-68ba7fee3385
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b6b5c0a0879580e5c1e084259b61ff206d49c896
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="applockmode-transact-sql"></a>APPLOCK_MODE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回锁所有者对特定应用程序资源所持有的锁模式。 APPLOCK_MODE 是一个应用程序锁函数，它对当前数据库进行操作。 应用程序锁的作用域是数据库。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
APPLOCK_MODE( 'database_principal' , 'resource_name' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>参数  
'database_principal'  
可将对数据库中对象的权限授予它们的用户、角色或应用程序角色。 该函数的调用方必须是 database_principal、dbo 或 db_owner 固定数据库角色的成员，才可成功调用该函数。
  
'resource_name'  
由客户端应用程序指定的锁资源名称。 应用程序必须确保该资源名称是唯一的。 指定的名称经过内部哈希运算后成为可以存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 锁管理器中的值。 resource_name 为 nvarchar(255)，无默认值。 resource_name 使用二进制比较并区分大小写，无论当前数据库的排序规则设置为何。
  
'lock_owner'  
锁的所有者，它是请求锁时所指定的 lock_owner 值。 lock_owner 为 nvarchar(32)，值可以是 Transaction（默认值）或 Session。
  
## <a name="return-types"></a>返回类型
**nvarchar(32)**
  
## <a name="return-value"></a>返回值
返回锁所有者对特定应用程序资源所持有的锁模式。 锁模式可以为下列值之一：
  
||||  
|-|-|-|  
|**NoLock**|**Update**|**\*SharedIntentExclusive**|  
|**IntentShared**|**IntentExclusive**|**\*UpdateIntentExclusive**|  
|**Shared**|**排他**||  
  
*该锁模式是其他锁模式的组合，并且无法使用 sp_getapplock 显式获取。
  
## <a name="function-properties"></a>函数属性
**Nondeterministic**
  
**Nonindexable**
  
**Nonparallelizable**
  
## <a name="examples"></a>示例  
具有不同会话的两个用户（用户 A 和用户 B）按以下顺序运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。
  
用户 A 运行：
  
```sql
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result int;  
EXEC @result=sp_getapplock  
    @DbPrincipal='public',  
    @Resource='Form1',  
    @LockMode='Shared',  
    @LockOwner='Transaction';  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
GO  
```  
  
然后用户 B 运行：
  
```sql
Use AdventureWorks2012;  
GO  
BEGIN TRAN;  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
--Result set: NoLock  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Shared', 'Transaction');  
--Result set: 1 (Lock is grantable.)  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: 0 (Lock is not grantable.)  
GO  
```  
  
然后用户 A 运行：
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
然后用户 B 运行：
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
然后用户 A 和用户 B 同时运行：
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>另请参阅
[APPLOCK_TEST (Transact-SQL)](../../t-sql/functions/applock-test-transact-sql.md)  
[sp_getapplock (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  
