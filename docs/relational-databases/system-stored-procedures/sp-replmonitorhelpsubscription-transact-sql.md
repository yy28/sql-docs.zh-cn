---
title: sp_replmonitorhelpsubscription (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
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
- sp_replmonitorhelpsubscription_TSQL
- sp_replmonitorhelpsubscription
helpviewer_keywords:
- sp_replmonitorhelpsubscription
ms.assetid: a681b2db-c82d-4624-a10c-396afb0ac42f
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 805b06a5346f10b2fb312828906ca2c923777022
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spreplmonitorhelpsubscription-transact-sql"></a>sp_replmonitorhelpsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回发布服务器上属于一个或多个发布的订阅的当前状态信息，并为每个返回的订阅返回一行。 在分发服务器的分发数据库上执行此存储过程，用于监视复制。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replmonitorhelpsubscription [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @mode = ] mode ]  
    [ , [ @topnum = ] topnum ]   
    [ , [ @exclude_anonymous = ] exclude_anonymous ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher** = ] **'***publisher***'**  
 正监视其状态的发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。 如果**null**，使用分发服务器的所有发布服务器返回信息。  
  
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
|NULL（默认值）|由复制来确定发布类型。|  
  
 [ **@mode** =]*模式*  
 返回订阅监视信息时要使用的筛选模式。 *模式*是**int**，并且可以为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**0** （默认值）|返回所有订阅。|  
|**1**|只返回带错误的订阅。|  
|**2**|只返回已生成在达到阈值度量指标时发出的警告的订阅。|  
|**3**|只返回带错误或已生成在达到阈值度量指标时发出的警告的订阅。|  
|**4**|返回前 25 坏的情况下执行的订阅。|  
|**5**|返回执行情况最差的 50 个订阅。|  
|**6**|只返回当前同步的订阅。|  
|**7**|只返回当前不同步的订阅。|  
  
 [ **@topnum** =] *topnum*  
 将结果集限制为返回数据顶部的指定订阅编号。 *topnum*是**int**，无默认值。  
  
 [ **@exclude_anonymous** =] *exclude_anonymous*  
 指示是否从结果集中排除匿名请求订阅。 *exclude_anonymous*是**位**，默认值为**0**; 的值**1**匿名订阅已排除的方式以及值为**0**意味着它们将包含的。  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 仅限内部使用。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**status**|**int**|检查与该发布关联的所有复制代理的状态，并返回按以下顺序找到的最高级状态：<br /><br /> **6** = 失败<br /><br /> **5** = 重试<br /><br /> **2** = 停止<br /><br /> **4** = 空闲<br /><br /> **3** = 正在进行<br /><br /> **1** = 启动|  
|**警告**|**int**|由属于该发布的订阅所生成的最大阈值警告，可以是下列一个或多个值进行逻辑或运算的结果。<br /><br /> **1** = 到期 – 在保留期阈值内尚未同步对事务发布的订阅。<br /><br /> **2** = 延迟-将数据从事务发布服务器复制到订阅服务器上所花费的时间超过阈值，以秒为单位。<br /><br /> **4** = mergeexpiration-在保留期阈值内尚未同步对合并发布的订阅。<br /><br /> **8** = mergefastrunduration-合并订阅的完成同步所花费的时间超过阈值，以秒为单位，通过快速网络连接。<br /><br /> **16** = mergeslowrunduration-合并订阅的完成同步所花费的时间超过阈值，以秒为单位，通过慢速或拨号网络连接。<br /><br /> **32** = mergefastrunspeed – 传送速率的行在合并订阅的同步过程中失败的快速网络连接通过维护阈值速率，单位为秒，每个行。<br /><br /> **64** = mergeslowrunspeed – 传送速率的行在合并订阅的同步过程中无法通过慢速或拨号网络连接维护阈值速率，单位为秒，每个行。|  
|**订阅服务器**|**sysname**|订阅服务器的名称。|  
|**subscriber_db**|**sysname**|用于订阅的数据库的名称。|  
|**publisher_db**|**sysname**|发布数据库的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**publication_type**|**int**|发布的类型，可以是下列值之一：<br /><br /> **0** = 事务发布<br /><br /> **1** = 快照发布<br /><br /> **2** = 合并发布|  
|**子类型**|**int**|订阅类型，可以是下列值之一：<br /><br /> **0** = 推送<br /><br /> **1** = 请求<br /><br /> **2** = 匿名|  
|**延迟**|**int**|在事务发布中，由日志读取器代理或分发代理传播的数据更改的最长滞后时间（以秒为单位）。|  
|**latencythreshold**|**int**|事务发布的最长滞后时间，高于此时间即产生警告。|  
|**agentnotrunning**|**int**|代理未运行的时间长度，以小时为单位。|  
|**agentnotrunningthreshold**|**int**|产生警告前代理未运行的时间长度，以小时为单位。|  
|**timetoexpiration**|**int**|订阅未同步时订阅过期前的时间长度，以小时为单位。|  
|**expirationthreshold**|**int**|订阅过期导致警告产生前的时间，以小时为单位。|  
|**last_distsync**|**datetime**|分发代理上次运行的日期时间。|  
|**distribution_agentname**|**sysname**|事务发布订阅的分发代理作业的名称。|  
|**mergeagentname**|**sysname**|合并发布订阅的合并代理作业的名称。|  
|**mergesubscriptionfriendlyname**|**sysname**|为订阅指定的友好名称。|  
|**mergeagentlocation**|**sysname**|运行合并代理的服务器的名称。|  
|**mergeconnectiontype**|**int**|将订阅同步到合并发布时使用的连接，可以是下列值之一：<br /><br /> **1** = 局域网 (LAN)<br /><br /> **2** = 拔号网络连接<br /><br /> **3** = web 同步。|  
|**mergePerformance**|**int**|订阅的上次同步相对于其所有同步而言的性能，用上次同步的传递速率除以之前所有传递速率的平均值。|  
|**mergerunspeed**|**float**|订阅的上次同步的传递速率。|  
|**mergerunduration**|**int**|完成订阅的上次同步的时间长度。|  
|**monitorranking**|**int**|用于对结果集中的订阅进行排序的排名值，可以是下列值之一：<br /><br /> 对于事务发布：<br /><br /> **60** = 错误<br /><br /> **56** = 警告： 关键的性能<br /><br /> **52** = 警告： 马上就要过期或已过期<br /><br /> **50** = 警告： 未初始化的订阅<br /><br /> **40** = 正在重试失败的命令<br /><br /> **30** = 未运行 （成功）<br /><br /> **20** = 运行 （从开始，运行或空闲）<br /><br /> 对于合并发布：<br /><br /> **60** = 错误<br /><br /> **56** = 警告： 关键的性能<br /><br /> **54** = 警告： 长时间运行的合并<br /><br /> **52** = 警告： 即将到期<br /><br /> **50** = 警告： 未初始化的订阅<br /><br /> **40** = 正在重试失败的命令<br /><br /> **30** = 运行 （从开始，运行或空闲）<br /><br /> **20** = 未运行 （成功）|  
|**distributionagentjobid**|**binary(16)**|事务发布订阅的分发代理作业的 ID。|  
|**mergeagentjobid**|**binary(16)**|合并发布订阅的合并代理作业的 ID。|  
|**distributionagentid**|**int**|订阅的分发代理作业的 ID。|  
|**distributionagentprofileid**|**int**|分发代理使用的代理配置文件的 ID。|  
|**mergeagentid**|**int**|订阅的合并代理作业的 ID。|  
|**mergeagentprofileid**|**int**|合并代理使用的代理配置文件的 ID。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_replmonitorhelpsubscription**用于所有类型的复制。  
  
 **sp_replmonitorhelpsubscription**基于状态的订阅，这由值的严重程度将结果集*monitorranking*。 例如，处于错误状态的所有订阅的各行排在处于警告状态的订阅的各行之上。  
  
## <a name="permissions"></a>权限  
 只有的成员**db_owner**或**replmonitor**在分发数据库上的固定的数据库角色可以执行**sp_replmonitorhelpsubscription**。  
  
## <a name="see-also"></a>另请参阅  
 [以编程方式监视复制](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
