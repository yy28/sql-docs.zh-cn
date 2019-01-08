---
title: sp_check_for_sync_trigger (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- filter_TSQL
- sp_check_for_sync_trigger
helpviewer_keywords:
- sp_check_for_sync_trigger
ms.assetid: 54a1e2fd-c40a-43d4-ac64-baed28ae4637
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9ac0fe99f835dae638cb65b24e569857fb77b098
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52759951"
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
 [ **@tabid =** ] '*tabid*  
 正对检查即时更新触发器的表的对象 ID。 *tabid*是**int** ，无默认值。  
  
 [ **@trigger_op =** ] '*trigger_output_parameters*输出  
 指定输出参数是否返回正在调用它的触发器的类型。 *trigger_output_parameters*是**char （10)** 可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**项**|INSERT 触发器|  
|**Upd**|UPDATE 触发器|  
|**Del**|DELETE 触发器|  
|NULL（默认值）||  
  
 [  **@fonpublisher =** ] *fonpublisher*  
 指定执行存储过程的位置。 *fonpublisher*是**位**，默认值为 0。 如果为 0，则在订阅服务器上执行；如果为 1，则在发布服务器上执行。  
  
## <a name="return-code-values"></a>返回代码值  
 0 指示在即时更新触发器的上下文中未调用此存储过程。 1 指示它即时更新触发器的上下文中调用，并且是中所返回的触发器的类型*@trigger_op*。  
  
## <a name="remarks"></a>备注  
 **sp_check_for_sync_trigger**快照复制和事务复制中使用。  
  
 **sp_check_for_sync_trigger**用于协调复制和用户定义触发器之间。 此存储过程确定它是否正在复制触发器的上下文中被调用。 例如，可以调用该过程**sp_check_for_sync_trigger**用户定义的触发器的正文中。 如果**sp_check_for_sync_trigger**返回**0**，在用户定义的触发器将继续进行处理。 如果**sp_check_for_sync_trigger**返回**1**，在用户定义的触发器退出。 这将确保当复制触发器更新表时不会激发用户定义触发器。  
  
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
 此外可以将代码添加到发布服务器; 表的触发器该代码非常相似，但是将调用**sp_check_for_sync_trigger**包含一个附加参数。  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int, @fonpublisher int  
SELECT @table_id = object_id('tablename')  
SELECT @fonpublisher = 1  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT, @fonpublisher  
IF @retcode = 1  
RETURN  
```  
  
## <a name="permissions"></a>权限  
 **sp_check_for_sync_trigger**可以由具有 SELECT 权限中的任何用户执行存储的过程[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)系统视图。  
  
## <a name="see-also"></a>请参阅  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
