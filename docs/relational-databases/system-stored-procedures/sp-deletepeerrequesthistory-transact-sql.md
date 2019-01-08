---
title: sp_deletepeerrequesthistory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletepeerrequesthistory
- sp_deletepeerrequesthistory_TSQL
helpviewer_keywords:
- sp_deletepeerrequesthistory
ms.assetid: 63a4ec6e-ce79-4bf1-9d37-5ac88f8d6beb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f5bb18d06fd8ab9545825174cba0723f0d553ee
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791519"
---
# <a name="spdeletepeerrequesthistory-transact-sql"></a>sp_deletepeerrequesthistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除与发布状态请求，其中包括请求历史记录相关的历史记录 ([MSpeer_request &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mspeer-request-transact-sql.md)) 以及响应历史记录 ([MSpeer_response &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mspeer-response-transact-sql.md))。在发布服务器参与对等复制拓扑的发布数据库上执行此存储的过程。 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_deletepeerrequesthistory [ @publication = ] 'publication'  
    [ , [ @request_id = ] request_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=** ] **'***发布*****  
 已向其发送状态请求的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@request_id=** ] *request_id*  
 指定单个状态请求，以便删除对该请求的所有响应。 *request_id*是**int**，默认值为 NULL。  
  
 [  **@cutoff_date=** ] *cutoff_date*  
 指定一个截止日期，该日期之前的所有早期响应记录都将被删除。 *cutoff_date*是**datetime**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_deletepeerrequesthistory**对等事务复制拓扑中使用。 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 执行时**sp_deletepeerrequesthistory**、 任一*request_id*或*cutoff_date*必须指定。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_deletepeerrequesthistory**。  
  
## <a name="see-also"></a>请参阅  
 [sp_helppeerrequests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)   
 [sp_helppeerresponses &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)   
 [sp_requestpeerresponse &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)  
  
  
