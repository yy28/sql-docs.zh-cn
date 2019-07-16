---
title: sp_replcmds (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replcmds_TSQL
- sp_replcmds
helpviewer_keywords:
- sp_replcmds
ms.assetid: 7e932f80-cc6e-4109-8db4-2b7c8828df73
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8aad9f67b155c1f247426053b948cc6dd29e4cbe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006897"
---
# <a name="spreplcmds-transact-sql"></a>sp_replcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回标记为要复制的事务的命令。 在发布服务器上对发布数据库执行此存储的过程。  
  
> [!IMPORTANT]  
>  **Sp_replcmds**应运行过程只是为了解决复制问题。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>参数  
`[ @maxtrans = ] maxtrans` 是要返回其信息的事务数。 *maxtrans*是**int**，默认值为**1**，它指定下一个等待分发的事务。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**文章 id**|**int**|项目的 ID。|  
|**partial_command**|**bit**|指示这是否为部分命令。|  
|**command**|**varbinary(1024)**|命令值。|  
|**xactid**|**binary(10)**|事务 id。|  
|**xact_seqno**|**varbinary(16)**|事务序列号。|  
|**publication_id**|**int**|发布 ID。|  
|**command_id**|**int**|中的命令 ID [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)。|  
|**command_type**|**int**|命令的类型。|  
|**originator_srvname**|**sysname**|发起事务的服务器。|  
|**originator_db**|**sysname**|发起事务的数据库。|  
|**pkHash**|**int**|仅限内部使用。|  
|**originator_publication_id**|**int**|发起事务的发布的 ID。|  
|**originator_db_version**|**int**|发起事务的数据库的版本。|  
|**originator_lsn**|**varbinary(16)**|标识初始发布中命令的日志序列号 (LSN)。|  
  
## <a name="remarks"></a>备注  
 **sp_replcmds**由日志读取器进程在事务复制中。  
  
 复制将在运行第一个客户端**sp_replcmds**日志读取器为给定数据库内。  
  
 此过程可以为所有者限定的表或未限定的表名（默认值）生成命令。 通过添加限定的表名，可将数据从特定用户在一个数据库中拥有的表复制到此用户在另一个数据库中拥有的表中。  
  
> [!NOTE]  
>  由于源数据库内的表名是由所有者名称限定的，所以目标数据库内的表所有者必须具有相同的所有者名称。  
  
 尝试运行的客户端**sp_replcmds**同一数据库中收到 18752 号错误，直到第一个客户端断开连接。 第一个客户端断开连接后，可以运行另一个客户端**sp_replcmds**，并成为新的日志读取器。  
  
 警告消息添加 18759 号既[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]错误日志和[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 应用程序日志，如果**sp_replcmds**无法复制文本命令，因为不是文本指针检索对同一事务中。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_replcmds**。  
  
## <a name="see-also"></a>请参阅  
 [错误消息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
