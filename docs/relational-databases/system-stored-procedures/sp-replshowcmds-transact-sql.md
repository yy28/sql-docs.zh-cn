---
title: sp_replshowcmds (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 39675a5c4e51a286f2888ef668a5debee04249a1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spreplshowcmds-transact-sql"></a>sp_replshowcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  以可读格式返回标记为复制的事务的命令。 **sp_replshowcmds**仅从日志 （包括当前连接） 的客户端连接根本无法阅读复制的事务可以运行。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>参数  
 [ **@maxtrans** =] *maxtrans*  
 要返回相关信息的事务的数量。 *maxtrans*是**int**，默认值为**1**，它指定挂起的复制的事务的最大数目**sp_replshowcmds**返回的信息。  
  
## <a name="result-sets"></a>结果集  
 **sp_replshowcmds**是返回有关发布数据库从其执行的信息的诊断过程。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|该命令的序列号。|  
|**originator_id**|**int**|ID 的命令发起方始终**0**。|  
|**publisher_database_id**|**int**|发布服务器数据库，始终 ID **0**。|  
|**article_id**|**int**|项目的 ID。|  
|**类型**|**int**|命令的类型。|  
|**command**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 命令。|  
  
## <a name="remarks"></a>注释  
 **sp_replshowcmds**事务复制中使用。  
  
 使用**sp_replshowcmds**，你可以查看当前的事务不分发的事务 （事务日志中剩余的未发送到分发服务器）。  
  
 运行的客户端**sp_replshowcmds**和**sp_replcmds**同一数据库中收到错误 18752。  
  
 若要避免此错误，第一个客户端必须断开连接，或者必须通过执行释放日志读取器以对客户端的角色**sp_replflush**。 所有客户端日志读取器，从已断开连接后**sp_replshowcmds**可成功运行。  
  
> [!NOTE]  
>  **sp_replshowcmds**应运行只是为了解决复制的问题。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_replshowcmds**。  
  
## <a name="see-also"></a>另请参阅  
 [错误消息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
