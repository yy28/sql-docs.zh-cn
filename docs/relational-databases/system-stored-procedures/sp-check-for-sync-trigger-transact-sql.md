---
title: "sp_check_for_sync_trigger (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- filter_TSQL
- sp_check_for_sync_trigger
helpviewer_keywords:
- sp_check_for_sync_trigger
ms.assetid: 54a1e2fd-c40a-43d4-ac64-baed28ae4637
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 586498365ee695ee5dc92252af47ad7706e1adfb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spcheckforsynctrigger-transact-sql"></a>sp_check_for_sync_trigger (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  确定是否正在用于立即更新订阅的复制触发器的上下文中调用用户定义的触发器或存储过程。 该存储过程在发布服务器的发布数据库中或在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_check_for_sync_trigger [ @tabid = ] 'tabid'   
    [ , [ @trigger_op = ] 'trigger_output_parameters' OUTPUT ]  
    [ , [ @fonpublisher = ] fonpublisher ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@tabid =** ]*tabid*  
 正对检查即时更新触发器的表的对象 ID。 *tabid*是**int**无默认值。  
  
 [ **@trigger_op =** ]*trigger_output_parameters*输出  
 指定输出参数是否返回正在调用它的触发器的类型。 *trigger_output_parameters*是**char （10)**和可以是下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**单元**|INSERT 触发器|  
|**Upd**|UPDATE 触发器|  
|**Del**|DELETE 触发器|  
|NULL（默认值）||  
  
 [  **@fonpublisher =** ] *fonpublisher*  
 指定执行存储过程的位置。 *fonpublisher*是**位**，默认值为 0。 如果为 0，则在订阅服务器上执行；如果为 1，则在发布服务器上执行。  
  
## <a name="return-code-values"></a>返回代码值  
 0 指示在即时更新触发器的上下文中未调用此存储过程。 1 表示它立即更新触发器的上下文中调用，并且是在所返回的触发器的类型 *@trigger_op* 。  
  
## <a name="remarks"></a>注释  
 **sp_check_for_sync_trigger**快照复制和事务复制中使用。  
  
 **sp_check_for_sync_trigger**用于协调之间复制和用户定义的触发器。 此存储过程确定它是否正在复制触发器的上下文中被调用。 例如，您可以调用过程**sp_check_for_sync_trigger**用户定义的触发器的正文中。 如果**sp_check_for_sync_trigger**返回**0**，该用户定义的触发器将继续处理。 如果**sp_check_for_sync_trigger**返回**1**，该用户定义的触发器退出。 这将确保当复制触发器更新表时不会激发用户定义触发器。  
  
## <a name="example"></a>示例  
 以下示例说明了可在订阅服务器表的触发器中使用的代码。  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int  
SELECT @table_id = object_id('tablename')  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT  
IF @retcode = 1  
RETURN  
```  
  
## <a name="example"></a>示例  
 此外可以将代码添加到发布服务器; 上的表的触发器代码将类似，但调用**sp_check_for_sync_trigger**包括一个附加参数。  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int, @fonpublisher int  
SELECT @table_id = object_id('tablename')  
SELECT @fonpublisher = 1  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT, @fonpublisher  
IF @retcode = 1  
RETURN  
```  
  
## <a name="permissions"></a>Permissions  
 **sp_check_for_sync_trigger**可以通过拥有 SELECT 权限中的任何用户执行存储的过程[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)系统视图。  
  
## <a name="see-also"></a>另请参阅  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
