---
title: sp_helppeerresponses （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f9303801527b3154585034e1097623ce073fb91f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82834383"
---
# <a name="sp_helppeerresponses-transact-sql"></a>sp_helppeerresponses (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回对等复制拓扑中参与者收到的特定状态请求的所有响应，其中请求是通过在拓扑中的任何已发布数据库上执行[sp_helppeerrequests](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)启动的。 此存储过程将对参与对等复制拓扑的发布服务器上的发布数据库执行。 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helppeerresponses [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>参数  
`[ @request_id = ] request_id`特定状态请求的 ID。 *request_id*为**int**，没有默认值。  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|状态请求的 ID。|  
|**对等**|**sysname**|生成响应的对等方的名称。|  
|**peer_db**|**sysname**|对等方上生成响应的数据库名称。|  
|**received_date**|**datetime**|请求程序收到对等方发送的响应的日期和时间。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_helppeerresponses**用于对等事务复制。  
  
 还原在对等拓扑中发布的数据库时，将使用**sp_helppeerresponses**过程。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_helppeerresponses**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_deletepeerrequesthistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
