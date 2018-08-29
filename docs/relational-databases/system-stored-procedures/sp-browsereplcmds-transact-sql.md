---
title: sp_browsereplcmds (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_browsereplcmds_TSQL
- sp_browsereplcmds
helpviewer_keywords:
- sp_browsereplcmds
ms.assetid: 30abcb41-1d18-4f43-a692-4c80914c0450
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 744f28362bcb64d0d4e294e464cbd94c26f13d60
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036551"
---
# <a name="spbrowsereplcmds-transact-sql"></a>sp_browsereplcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回分发数据库中存储的可读版本复制命令的结果集，并将其用作诊断工具。 此存储过程在分发服务器上对分发数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_browsereplcmds [ [ @xact_seqno_start = ] 'xact_seqno_start' ]  
    [ , [ @xact_seqno_end = ] 'xact_seqno_end' ]   
    [ , [ @originator_id = ] 'originator_id' ]  
    [ , [ @publisher_database_id = ] 'publisher_database_id' ]  
    [ , [ @article_id = ] 'article_id' ]  
    [ , [ @command_id= ] command_id ]  
    [ , [ @agent_id = ] agent_id ]  
    [ , [ @compatibility_level = ] compatibility_level ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@xact_seqno_start =**] **'***xact_seqno_start*****  
 指定要返回的取值最低的精确序列号。 *xact_seqno_start*是**nchar(22)**，默认值为 0x00000000000000000000。  
  
 [  **@xact_seqno_end =**] **'***xact_seqno_end*****  
 指定要返回的取值最高的精确序列号。 *xact_seqno_end*是**nchar(22)**，默认值为 0xFFFFFFFFFFFFFFFFFFFF。  
  
 [  **@originator_id =**] **'***originator_id*****  
 指定如果具有指定的命令*originator_id*返回。 *originator_id*是**int**，默认值为 NULL。  
  
 [  **@publisher_database_id =**] **'***publisher_database_id*****  
 指定如果具有指定的命令*publisher_database_id*返回。 *publisher_database_id*是**int**，默认值为 NULL。  
  
 [  **@article_id =**] **'***article_id*****  
 指定如果具有指定的命令*article_id*返回。 *article_id*是**int**，默认值为 NULL。  
  
 [  **@command_id =**] *command_id*  
 是中的命令的位置[MSrepl_commands &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)要解码。 *command_id*是**int**，默认值为 NULL。 如果指定，则必须还，指定所有其他参数和*xact_seqno_start*必须与相同*xact_seqno_end*。  
  
 [  **@agent_id =**] *agent_id*  
 指定仅返回特定复制代理的命令。 *agent_id*是**int**，默认值为 NULL。  
  
 [  **@compatibility_level =**] *compatibility_level*  
 是的版本[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]依据*compatibility_level*是**int**，默认值为 9000000。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**varbinary(16)**|该命令的序列号。|  
|**originator_srvname**|**sysname**|发起事务的服务器。|  
|**originator_db**|**sysname**|发起事务的数据库。|  
|**article_id**|**int**|项目的 ID。|  
|**类型**|**int**|命令的类型。|  
|**partial_command**|**bit**|指示是否为部分命令。|  
|**hashkey**|**int**|仅限内部使用。|  
|**originator_publication_id**|**int**|发起事务的发布的 ID。|  
|**originator_db_version**|**int**|发起事务的数据库的版本。|  
|**originator_lsn**|**varbinary(16)**|标识初始发布中命令的日志序列号 (LSN)。 在对等事务复制中使用。|  
|**command**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 命令。|  
|**command_id**|**int**|中的命令 ID [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)。|  
  
 在结果集中，长命令可以拆分为若干行。  
  
## <a name="remarks"></a>Remarks  
 **sp_browsereplcmds**事务复制中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定服务器角色或成员**db_owner**或**replmonitor**上分发数据库的固定的数据库角色可以执行**sp_browsereplcmds**。  
  
## <a name="see-also"></a>请参阅  
 [sp_replcmds (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replshowcmds &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
