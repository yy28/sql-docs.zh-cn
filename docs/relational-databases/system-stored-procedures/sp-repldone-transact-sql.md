---
title: sp_repldone (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldone
- sp_repldone_TSQL
helpviewer_keywords:
- sp_repldone
ms.assetid: 045d3cd1-712b-44b7-a56a-c9438d4077b9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aaeebd1aa2d6fe4ea443c7ed18ac157135ae4d64
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747741"
---
# <a name="sprepldone-transact-sql"></a>sp_repldone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新用于标识服务器的最后一个已分发事务的记录。 在发布服务器上对发布数据库执行此存储的过程。  
  
> [!CAUTION]  
>  如果您执行**sp_repldone**手动，您可能会导致无效的顺序和传递的事务一致性。 **sp_repldone**仅应该用于排除复制故障的有经验的复制支持专业人员的指导。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_repldone [ @xactid= ] xactid   
        , [ @xact_seqno= ] xact_seqno   
    [ , [ @numtrans= ] numtrans ]   
    [ , [ @time= ] time   
    [ , [ @reset= ] reset ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@xactid=**] *xactid*  
 是服务器的最后一个分布式事务的第一个记录的日志序列号 (LSN)。 *xactid*是**binary(10)**，无默认值。  
  
 [  **@xact_seqno=**] *xact_seqno*  
 是服务器的最后一个分布式事务的最后一个记录的 LSN。 *xact_seqno*是**binary(10)**，无默认值。  
  
 [  **@numtrans=**] *numtrans*  
 是分布的事务数。 *对于 numtrans*是**int**，无默认值。  
  
 [  **@time=**]*时间*  
 分发最后一批事务所需的毫秒数（如果提供）。 *时间*是**int**，无默认值。  
  
 [  **@reset=**]*重置*  
 重置状态。 *重置*是**int**，无默认值。 如果**1**、 所有已复制事务日志中的标记为已分发。 如果**0**、 事务日志将重置为第一个复制的事务和没有复制的事务标记为已分发。 *重置*仅当同时*xactid*并*xact_seqno*均为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_repldone**事务复制中使用。  
  
 **sp_repldone**由日志读取器进程用来跟踪哪些事务已分发。  
  
 与**sp_repldone**，您可以手动通知服务器已 （发送到分发服务器），复制事务。 它还允许您更改被标记为下一个等待复制的事务。 您可以在已复制事务的列表中前后移动。 （所有小于或等于该事务的事务都将标记为已分发。）  
  
 所需的参数*xactid*并*xact_seqno*可以通过使用获取**sp_repltrans**或者**sp_replcmds**。  
  
## <a name="permissions"></a>权限  
 成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_repldone**。  
  
## <a name="examples"></a>示例  
 时*xactid*为 NULL， *xact_seqno*为 NULL，并*重置*是**1**、 所有已复制事务日志中的标记为已分发。 当事务日志中存在不再有效的复制事务并且想截断该日志时，此过程很有用，例如：  
  
```  
EXEC sp_repldone @xactid = NULL, @xact_segno = NULL, @numtrans = 0,     @time = 0, @reset = 1  
```  
  
> [!CAUTION]  
>  可以在紧急情况下使用此过程，以允许在有事务挂起复制时截断事务日志。  
  
## <a name="see-also"></a>请参阅  
 [sp_replcmds (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replflush &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
