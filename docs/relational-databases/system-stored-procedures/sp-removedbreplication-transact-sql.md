---
title: sp_removedbreplication (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_removedbreplication
- sp_removedbreplication_TSQL
helpviewer_keywords:
- sp_removedbreplication
ms.assetid: cb98d571-d1eb-467b-91f7-a6e091009672
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7d3931ff867ef1475165eb6cbac97f4ba4564bf9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006953"
---
# <a name="spremovedbreplication-transact-sql"></a>sp_removedbreplication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此存储过程将删除 SQL Server 发布服务器实例的发布数据库上或 SQL Server 订阅服务器实例的订阅数据库上的所有复制对象。 在相应的数据库中执行，或如果是在另一个数据库上下文的同一个实例上执行，请指定应删除复制对象的数据库。 此过程不会从其他数据库（例如，分发数据库）中删除对象。  
  
> [!NOTE]  
>  只有当其他删除复制对象的方法都失败后，才应当使用此过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_removedbreplication [ [ @dbname = ] 'dbname' ]  
    [ , [ @type = ] type ]   
```  
  
## <a name="arguments"></a>参数  
`[ @dbname = ] 'dbname'` 是数据库的名称。 *dbname* 的数据类型为 **sysname**，默认值为 NULL。 此参数值为 NULL 时，将使用当前数据库。  
  
`[ @type = ] type` 是的复制的数据库内要被删除的对象的类型。 *类型*是**nvarchar(5)** 可以是下列值之一。  
  
|||  
|-|-|  
|**tran**|删除事务复制发布对象。|  
|**合并**|删除合并复制发布对象。|  
|**同时**（默认值）|删除所有复制发布对象。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_removedbreplication**用于所有类型的复制。  
  
 **sp_removedbreplication**还原复制的数据库，无需还原没有复制对象时非常有用。  
  
 **sp_removedbreplication**不能使用针对数据库被标记为只读的。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_removedbreplication](../../relational-databases/replication/codesnippet/tsql/sp-removedbreplication-t_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_removedbreplication**。  
  
## <a name="example"></a>示例  
  
```  
-- Remove replication objects from the subscription database on MYSUB.  
DECLARE @subscriptionDB AS sysname  
SET @subscriptionDB = N'AdventureWorksReplica'  
  
-- Remove replication objects from a subscription database (if necessary).  
USE master  
EXEC sp_removedbreplication @subscriptionDB  
GO  
  
```  
  
## <a name="see-also"></a>请参阅  
 [禁用发布和分发](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
