---
title: sp_replmonitorhelppublication (Transact SQL) |Microsoft 文档
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
- sp_replmonitorhelppublication_TSQL
- sp_replmonitorhelppublication
helpviewer_keywords:
- sp_replmonitorhelppublication
ms.assetid: 7928c50c-617f-41c5-9e0f-4e42e8be55dc
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e6802b8acc592e83cedd78a233cbd8f5cbb7dd26
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spreplmonitorhelppublication-transact-sql"></a>sp_replmonitorhelppublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回发布服务器上一个或多个发布的当前状态信息。 在分发服务器的分发数据库上执行此存储过程，用于监视复制。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replmonitorhelppublication [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db'   
    [ , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher** = ] **'***publisher***'**  
 正监视其状态的发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。 如果**null**，将使用分发服务器的所有发布服务器返回的信息。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 已发布数据库的名称。 *publisher_db*是**sysname**，默认值为 NULL。 如果为 NULL，则返回发布服务器上所有已发布数据库的信息。  
  
 [ **@publication** = ] **'***publication***'**  
 要监视的发布的名称。 *发布*是**sysname**，默认值为 NULL。  
  
 [ **@publication_type** =] *publication_type*  
 发布的类型。 *publication_type*是**int**，并且可以为这些值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**0**|事务发布。|  
|**1**|快照发布。|  
|**2**|合并发布。|  
|NULL（默认值）|复制尝试确定发布类型。|  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 仅限内部使用。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_db**|**sysname**|发布服务器的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**publication_type**|**int**|发布的类型，可以是以下值之一。<br /><br /> **0** = 事务发布<br /><br /> **1** = 快照发布<br /><br /> **2** = 合并发布|  
|**status**|**int**|与发布关联的所有复制代理的最大值求值状态，可以是下列值之一。<br /><br /> **1** = 启动<br /><br /> **2** = 成功<br /><br /> **3** = 正在进行<br /><br /> **4** = 空闲<br /><br /> **5** = 重试<br /><br /> **6** = 失败|  
|**警告**|**int**|由属于该发布的订阅所生成的最大阈值警告，可以是下列一个或多个值进行逻辑或运算的结果。<br /><br /> **1** = 到期 – 在保留期阈值内尚未同步对事务发布的订阅。<br /><br /> **2** = 延迟-将数据从事务发布服务器复制到订阅服务器上所花费的时间超过阈值，以秒为单位。<br /><br /> **4** = mergeexpiration-在保留期阈值内尚未同步对合并发布的订阅。<br /><br /> **8** = mergefastrunduration-合并订阅的完成同步所花费的时间超过阈值，以秒为单位，通过快速网络连接。<br /><br /> **16** = mergeslowrunduration-合并订阅的完成同步所花费的时间超过阈值，以秒为单位，通过慢速或拨号网络连接。<br /><br /> **32** = mergefastrunspeed – 传送速率的行在合并订阅的同步过程中失败的快速网络连接通过维护阈值速率，单位为秒，每个行。<br /><br /> **64** = mergeslowrunspeed – 传送速率的行在合并订阅的同步过程中无法通过慢速或拨号网络连接维护阈值速率，单位为秒，每个行。|  
|**worst_latency**|**int**|在事务发布中，由日志读取器代理或分发代理传播的数据更改的最长滞后时间（以秒为单位）。|  
|**best_latency**|**int**|在事务发布中，由日志读取器代理或分发代理传播的数据更改的最短滞后时间（以秒为单位）。|  
|**average_latency**|**int**|在事务发布中，由日志读取器代理或分发代理传播的数据更改的平均滞后时间（以秒为单位）。|  
|**last_distsync**|**datetime**|上一次分发代理运行的日期时间。|  
|**保持期**|**int**|发布的保持期。|  
|**latencythreshold**|**int**|为事务发布设置的滞后时间阈值。|  
|**expirationthreshold**|**int**|为合并发布设置的过期阈值。|  
|**agentnotrunningthreshold**|**int**|为代理设置的无需运行的最长时间阈值。|  
|**subscriptioncount**|**int**|对发布的订阅数。|  
|**runningdistagentcount**|**int**|运行发布的分发代理的数量|  
|**snapshot_agentname**|**sysname**|发布的快照代理作业的名称。|  
|**logreader_agentname**|**sysname**|事务发布的日志读取器代理作业的名称。|  
|**qreader_agentname**|**sysname**|支持排队更新的事务发布的队列读取器代理作业的名称。|  
|**worst_runspeedPerf**|**int**|合并发布的最长同步时间。|  
|**best_runspeedPerf**|**int**|是为合并发布的最短同步时间。|  
|**average_runspeedPerf**|**int**|合并发布的平均同步时间。|  
|**retention_period_unit**|**int**|是用于 express 的单位*保留*。|  
|**publisher**|**sysname**|发布内容的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_replmonitorhelppublication**用于所有类型的复制。  
  
## <a name="permissions"></a>权限  
 只有的成员**db_owner**或**replmonitor**在分发数据库上的固定的数据库角色可以执行**sp_replmonitorhelppublication**。  
  
## <a name="see-also"></a>另请参阅  
 [以编程方式监视复制](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
