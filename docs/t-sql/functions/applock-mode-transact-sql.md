---
title: "APPLOCK_MODE (Transact SQL) |Microsoft 文档"
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
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ceec0a5465187e1b470bd9eb8b1039a5b3d60aae
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="applockmode-transact-sql"></a>APPLOCK_MODE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回锁所有者对特定应用程序资源所持有的锁模式。 APPLOCK_MODE 是一个应用程序锁函数，它对当前数据库进行操作。 应用程序锁的作用域是数据库。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
APPLOCK_MODE( 'database_principal' , 'resource_name' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>参数  
*database_principal*  
可将对数据库中对象的权限授予它们的用户、角色或应用程序角色。 该函数的调用方必须是属于*database_principal*，dbo 或 db_owner 固定数据库角色，以成功调用函数。
  
*resource_name*  
由客户端应用程序指定的锁资源名称。 应用程序必须确保该资源名称是唯一的。 指定的名称经过内部哈希运算后成为可以存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 锁管理器中的值。 *resource_name*是**nvarchar （255)**无默认值。 *resource_name*是二进制比较，并且区分大小写，无论当前数据库的排序规则设置如何。
  
*lock_owner*  
所有者的锁定，这是*lock_owner*时请求该锁的值。 *lock_owner*是**nvarchar(32)**，和值可以是**事务**（默认值） 或**会话**。
  
## <a name="return-types"></a>返回类型
**nvarchar(32)**
  
## <a name="return-value"></a>返回值
返回锁所有者对特定应用程序资源所持有的锁模式。 锁模式可以为下列值之一：
  
||||  
|-|-|-|  
|**NoLock**|**Update**|**\*SharedIntentExclusive**|  
|**IntentShared**|**IntentExclusive**|**\*UpdateIntentExclusive**|  
|**共享**|**排他**||  
  
*该锁模式是其他锁模式的组合，并且无法使用 sp_getapplock 显式获取。
  
## <a name="function-properties"></a>函数属性
**具有不确定性**
  
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
[APPLOCK_TEST &#40;Transact SQL &#41;](../../t-sql/functions/applock-test-transact-sql.md)  
[sp_getapplock &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  

