---
title: sp_replshowcmds (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 96a32ea04fc53f1a0bf3a842a5e68cde5586ac29
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770883"
---
# <a name="spreplshowcmds-transact-sql"></a>sp_replshowcmds (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  以可读格式返回标记为复制的事务的命令。 仅当客户端连接 (包括当前连接) 不从日志中读取复制的事务时, 才能运行**sp_replshowcmds** 。 此存储过程在发布服务器上对发布数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>参数  
`[ @maxtrans = ] maxtrans`要返回其信息的事务数。 *maxtrans*的值为**int**, 默认值为**1**, 该值指定**sp_replshowcmds**为其返回信息的最大事务数。  
  
## <a name="result-sets"></a>结果集  
 **sp_replshowcmds**是一个诊断过程, 该过程返回有关从中执行它的发布数据库的信息。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|命令的序列号。|  
|**originator_id**|**int**|命令发起方的 ID, 始终为**0**。|  
|**publisher_database_id**|**int**|发布服务器数据库的 ID, 始终为**0**。|  
|**article_id**|**int**|项目的 ID。|  
|**type**|**int**|命令的类型。|  
|**command**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)]command.|  
  
## <a name="remarks"></a>备注  
 **sp_replshowcmds**用于事务复制。  
  
 使用**sp_replshowcmds**, 可以查看当前未分发的事务 (事务日志中尚未发送到分发服务器的事务)。  
  
 在同一数据库中运行**sp_replshowcmds**和**sp_replcmds**的客户端将收到错误18752。  
  
 若要避免此错误, 必须通过执行**sp_replflush**来断开第一个客户端的连接或客户端作为日志读取器的角色。 在所有客户端都与日志读取器断开连接后, **sp_replshowcmds**可以成功运行。  
  
> [!NOTE]  
>  **sp_replshowcmds**应仅用于排查复制问题。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_replshowcmds**。  
  
## <a name="see-also"></a>请参阅  
 [错误消息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
