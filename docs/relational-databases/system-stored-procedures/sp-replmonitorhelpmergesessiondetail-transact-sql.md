---
title: sp_replmonitorhelpmergesessiondetail (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
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
- sp_replmonitorhelpmergesessiondetail
- sp_replmonitorhelpmergesessiondetail_TSQL
helpviewer_keywords:
- sp_replmonitorhelpmergesessiondetail
ms.assetid: 805c92fc-3169-410c-984d-f37e063b791d
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 44bb40f02a7e8f537141f34db3bf4cc38c8b093f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spreplmonitorhelpmergesessiondetail-transact-sql"></a>sp_replmonitorhelpmergesessiondetail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关特定复制合并代理会话的项目级详细信息，该会话用于监视合并复制。 结果集包括在会话过程中被同步的每个项目的详细信息行。 另外还包括提供会话初始化的行以及汇总上载和下载会话阶段的行。 此存储过程针对分发服务器的分发数据库或订阅服务器的订阅数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replmonitorhelpmergesessiondetail [ @session_id = ] session_id  
```  
  
## <a name="arguments"></a>参数  
 [ **@session_id** = ] *session_id*  
 指定一个代理会话。 *session_id*是**int**无默认值。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**PhaseID**|**int**|同步会话的阶段，可以是下列值之一：<br /><br /> **0** = 初始化或摘要行<br /><br /> **1** = 上载<br /><br /> **2** = 下载|  
|**ArticleName**|**sysname**|被同步的项目的名称。 **ArticleName**还包含在结果集中的行，无法表示文章详细信息的摘要信息。|  
|**PercentComplete**|**decimal**|指示当前正在运行或已失败的会话中，给定的项目详细信息行中应用的全部更改的百分比。|  
|**RelativeCost**|**decimal**|指示同步项目所花时间占会话的同步总时间的百分比。|  
|**Duration**|**int**|代理会话的长度。|  
|**Inserts**|**int**|会话中的插入数。|  
|**Updates**|**int**|会话中的更新数。|  
|**Deletes**|**int**|会话中的删除数。|  
|**冲突**|**int**|会话中发生的冲突数。|  
|**错误 Id**|**int**|会话错误的 ID。|  
|**SeqNo**|**int**|结果集中会话的顺序。|  
|**RowType**|**int**|指示结果集中的每一行所提供的信息类型。<br /><br /> **0** = 初始化<br /><br /> **1** = 上载摘要<br /><br /> **2** = 文章上载详细信息<br /><br /> **3** = 下载摘要<br /><br /> **4** = 文章下载详细信息|  
|**架构**|**int**|会话中的架构更改数。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_replmonitorhelpmergesessiondetail**用于监视合并复制。  
  
 当对订阅服务器上，执行**sp_replmonitorhelpmergesessiondetail**仅返回有关最近使用的 5 的合并代理会话的详细的信息。  
  
## <a name="permissions"></a>权限  
 只有的成员**db_owner**或**replmonitor**分发服务器上的分发数据库上或订阅服务器上的订阅数据库上的固定的数据库角色可以执行**sp_replmonitorhelpmergesessiondetail**。  
  
## <a name="see-also"></a>另请参阅  
 [以编程方式监视复制](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
