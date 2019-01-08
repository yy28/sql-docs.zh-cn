---
title: sp_helppeerresponses (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerresponses_TSQL
- sp_helppeerresponses
helpviewer_keywords:
- sp_helppeerresponses
ms.assetid: e55789d1-43fb-4a37-9e5e-60ccef122a5d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a3cce9577f609a0216b5d96e82eeacbdc295b26d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802199"
---
# <a name="sphelppeerresponses-transact-sql"></a>sp_helppeerresponses (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回从通过执行其中启动请求的对等复制拓扑中参与者收到的特定状态请求的所有响应[sp_helppeerrequests](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)拓扑中任意已发布数据库。 此存储过程将对参与对等复制拓扑的发布服务器上的发布数据库执行。 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helppeerresponses [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>参数  
 [ **@request_id**=] *request_id*  
 特定状态请求的 ID。 *request_id*是**int**，无默认值。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|状态请求的 ID。|  
|**对等**|**sysname**|生成响应的对等方的名称。|  
|**peer_db**|**sysname**|对等方上生成响应的数据库名称。|  
|**received_date**|**datetime**|请求程序收到对等方发送的响应的日期和时间。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_helppeerresponses**对等事务复制中使用。  
  
 **sp_helppeerresponses**时还原发布的数据库在对等拓扑中使用过程。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_helppeerresponses**。  
  
## <a name="see-also"></a>请参阅  
 [sp_deletepeerrequesthistory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
