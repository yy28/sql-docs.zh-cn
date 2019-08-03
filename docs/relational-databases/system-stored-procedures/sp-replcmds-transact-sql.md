---
title: sp_replcmds (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 3d60de0f459ec1224f6023e8ee848227fdc17ece
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771010"
---
# <a name="spreplcmds-transact-sql"></a>sp_replcmds (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  返回标记为要复制的事务的命令。 此存储过程在发布服务器上对发布数据库执行。  
  
> [!IMPORTANT]  
>  **Sp_replcmds**过程应仅用于排查复制问题。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>参数  
`[ @maxtrans = ] maxtrans`要返回其相关信息的事务数。 *maxtrans*的值为**int**, 默认值为**1**, 表示下一个等待分发的事务。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**文章 id**|**int**|项目的 ID。|  
|**partial_command**|**bit**|指示这是否为部分命令。|  
|**command**|**varbinary(1024)**|命令值。|  
|**xactid**|**binary(10)**|事务 ID。|  
|**xact_seqno**|**varbinary(16)**|事务序列号。|  
|**publication_id**|**int**|发布 ID。|  
|**command_id**|**int**|[MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)中的命令 ID。|  
|**command_type**|**int**|命令的类型。|  
|**originator_srvname**|**sysname**|发起事务的服务器。|  
|**originator_db**|**sysname**|发起事务的数据库。|  
|**pkHash**|**int**|仅限内部使用。|  
|**originator_publication_id**|**int**|发起事务的发布的 ID。|  
|**originator_db_version**|**int**|发起事务的数据库的版本。|  
|**originator_lsn**|**varbinary(16)**|标识初始发布中命令的日志序列号 (LSN)。|  
  
## <a name="remarks"></a>备注  
 **sp_replcmds**由日志读取器进程在事务复制中使用。  
  
 复制将给定数据库内运行**sp_replcmds**的第一个客户端视为日志读取器。  
  
 此过程可以为所有者限定的表或未限定的表名（默认值）生成命令。 通过添加限定的表名，可将数据从特定用户在一个数据库中拥有的表复制到此用户在另一个数据库中拥有的表中。  
  
> [!NOTE]  
>  由于源数据库内的表名是由所有者名称限定的，所以目标数据库内的表所有者必须具有相同的所有者名称。  
  
 如果客户端尝试在同一数据库内运行**sp_replcmds** , 则在第一个客户端断开连接之前, 会收到错误18752。 第一个客户端断开连接后, 其他客户端可以运行**sp_replcmds**, 并成为新的日志读取器。  
  
 如果**sp_replcmds**无法复制文本命令, 则将在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]错误日志和[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 应用程序日志中添加一条警告消息编号 18759, 因为在同一事务所.  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_replcmds**。  
  
## <a name="see-also"></a>请参阅  
 [错误消息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
