---
title: "删除队列 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP QUEUE
- DROP_QUEUE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dropping queues
- queues [Service Broker], removing
- deleting queues
- DROP QUEUE statement
- removing queues
ms.assetid: fd866520-ca00-477d-b2e9-0110e9610ed4
caps.latest.revision: "33"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3be4f36943d6e25bb520a28593d009e7a8373c48
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
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
{  
    [ database_name . [ schema_name ] . | schema_name . ]  
        queue_name  
}  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 数据库的名称，此数据库包含要删除的队列。 如果没有*database_name*提供，则默认为当前数据库。  
  
 *schema_name (object)*  
 架构的名称，此架构拥有要删除的队列。 如果没有*schema_name*提供，则默认为当前用户的默认架构。  
  
 *queue_name*  
 要删除的队列的名称。  
  
## <a name="remarks"></a>注释  
 如果有任何服务正在引用一个队列，则不能删除该队列。  
  
## <a name="permissions"></a>权限  
 删除队列的权限默认为队列的成员的所有者**db_ddladmin**或**db_owner**固定数据库角色和成员的**sysadmin**固定服务器角色。  
  
## <a name="examples"></a>示例  
 下面的示例删除**ExpenseQueue**从当前数据库的队列。  
  
```  
DROP QUEUE ExpenseQueue ;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE QUEUE (Transact SQL)](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER 队列 &#40;Transact SQL &#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
