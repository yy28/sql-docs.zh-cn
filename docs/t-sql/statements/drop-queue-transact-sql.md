---
title: DROP QUEUE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP QUEUE
- DROP_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping queues
- queues [Service Broker], removing
- deleting queues
- DROP QUEUE statement
- removing queues
ms.assetid: fd866520-ca00-477d-b2e9-0110e9610ed4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 297ef4c06b88d02e3c1a28829c7223d49c8ecee6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65503706"
---
# <a name="drop-queue-transact-sql"></a>DROP QUEUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除一个现有队列。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP QUEUE <object>  
[ ; ]  
  
<object> ::=  
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 数据库的名称，此数据库包含要删除的队列。 如果未提供 database_name，则默认为当前数据库  。  
  
 schema_name（对象）   
 架构的名称，此架构拥有要删除的队列。 如果未提供 schema_name，则默认为当前用户的默认架构  。  
  
 queue_name   
 要删除的队列的名称。  
  
## <a name="remarks"></a>Remarks  
 如果有任何服务正在引用一个队列，则不能删除该队列。  
  
## <a name="permissions"></a>权限  
 默认情况下，队列所有者、**db_ddladmin** 或 **db_owner** 固定数据库角色的成员以及 **sysadmin** 固定服务器角色的成员拥有删除队列的权限。  
  
## <a name="examples"></a>示例  
 下面的示例从当前数据库中删除 **ExpenseQueue** 队列。  
  
```  
DROP QUEUE ExpenseQueue ;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE QUEUE (Transact SQL)](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE (Transact SQL)](../../t-sql/statements/alter-queue-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
