---
title: sp_setsubscriptionxactseqno (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setsubscriptionxactseqno
- sp_setsubscriptionxactseqno_TSQL
helpviewer_keywords:
- sp_setsubscriptionxactseqno
ms.assetid: cdb4e0ba-5370-4905-b03f-0b0c6f080ca6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 27a7f35a915e2bff62932124aef64984a63cbd0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021082"
---
# <a name="spsetsubscriptionxactseqno-transact-sql"></a>sp_setsubscriptionxactseqno (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在故障排除期间用于指定最后传送的事务使用允许分发代理以开始在下一个事务下提供的日志序列号 (LSN)。 在重新启动，分发代理返回的事务大于此水印 (LSN) 从分发数据库缓存 (msrepl_commands)。 此存储过程在订阅服务器的订阅数据库中执行。 非 SQL Server 订阅服务器不支持该过程。  
  
> [!CAUTION]  
>  如果未正确使用此存储过程或指定了错误的 LSN 值，则将导致分发代理还原已应用于订阅服务器的更改，或跳过所有剩余的更改。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_setsubscriptionxactseqno [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @xact_seqno = ] xact_seqno   
```  
  
## <a name="arguments"></a>参数  
`[ @publisher = ] 'publisher'` 是发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
`[ @publisher_db = ] 'publisher_db'` 是发布数据库的名称。 *publisher_db*是**sysname**，无默认值。 对于非 SQL Server 发布服务器， *publisher_db*是分发数据库的名称。  
  
`[ @publication = ] 'publication'` 是发布的名称。 *发布*是**sysname**，无默认值。 当通过多个发布共享分发代理时，必须指定值为 ALL*发布*。  
  
`[ @xact_seqno = ] xact_seqno` 是要应用于订阅服务器上的分发服务器上的下一个事务的 LSN。 *xact_seqno*是**varbinary(16)** ，无默认值。  
  
## <a name="result-set"></a>结果集  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**ORIGINAL XACT_SEQNO**|**varbinary(16)**|要应用于订阅服务器的下一个事务的原始 LSN。|  
|**UPDATED XACT_SEQNO**|**varbinary(16)**|要应用于订阅服务器的下一个事务的更新后的 LSN。|  
|**订阅流计数**|**int**|上次同步期间使用的订阅流数。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_setsubscriptionxactseqno**事务复制中使用。  
  
 **sp_setsubscriptionxactseqno**不能对等事务复制拓扑中使用。  
  
 **sp_setsubscriptionxactseqno**可用于跳过导致错误的特定事务时在订阅服务器上进行应用。 故障时和分发代理停止后，请调用[sp_helpsubscriptionerrors &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpsubscriptionerrors-transact-sql.md)检索失败的事务的 xact_seqno 值，然后调用的分发服务器上**sp_setsubscriptionxactseqno**，将此值传递*xact_seqno*。 这将确保只处理此 LSN 之后的命令。  
  
 指定的值**0**有关*xact_seqno*将分发数据库中的所有挂起的命令传送到订阅服务器上。  
  
 **sp_setsubscriptionxactseqno**如果分发代理使用多订阅流可能会失败。  
  
 如果出现此错误，必须运行使用单个订阅流的分发代理。 有关详细信息，请参阅 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_setsubscriptionxactseqno**。  
  
## <a name="see-more"></a>查看详细信息

[博客：如何跳过的事务](https://repltalk.com/2019/05/28/how-to-skip-a-transaction/)  
