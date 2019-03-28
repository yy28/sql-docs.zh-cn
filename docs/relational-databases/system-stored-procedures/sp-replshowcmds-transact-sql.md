---
title: sp_replshowcmds (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e73b67cce73005b7a992c09a436dbda1db5c4e52
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526609"
---
# <a name="spreplshowcmds-transact-sql"></a>sp_replshowcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  以可读格式返回标记为复制的事务的命令。 **sp_replshowcmds**仅客户端连接 （包括当前连接） 无法阅读日志从复制的事务可以运行。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>参数  
`[ @maxtrans = ] maxtrans` 是要返回信息的事务数。 *maxtrans*是**int**，默认值为**1**，它指定的最大挂起复制的事务数**sp_replshowcmds**返回的信息。  
  
## <a name="result-sets"></a>结果集  
 **sp_replshowcmds**是一个诊断过程返回有关从中执行发布数据库的信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|该命令的序列号。|  
|**originator_id**|**int**|命令始发者始终 ID **0**。|  
|**publisher_database_id**|**int**|ID 的发布服务器数据库，始终**0**。|  
|**article_id**|**int**|项目的 ID。|  
|**类型**|**int**|命令的类型。|  
|**command**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 命令。|  
  
## <a name="remarks"></a>备注  
 **sp_replshowcmds**事务复制中使用。  
  
 使用**sp_replshowcmds**，可以查看当前未分发的事务 （事务日志中尚未发送到分发服务器的）。  
  
 运行的客户端**sp_replshowcmds**并**sp_replcmds**同一数据库中收到 18752 号错误。  
  
 若要避免此错误，第一个客户端必须断开连接或作为日志读取器的客户端角色必须通过执行释放**sp_replflush**。 所有客户端已断开连接的日志读取器从后**sp_replshowcmds**可以成功运行。  
  
> [!NOTE]  
>  **sp_replshowcmds**应运行只是为了解决复制问题。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_replshowcmds**。  
  
## <a name="see-also"></a>请参阅  
 [错误消息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
