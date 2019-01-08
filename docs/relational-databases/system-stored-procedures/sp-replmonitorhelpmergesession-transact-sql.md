---
title: sp_replmonitorhelpmergesession (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpmergesession_TSQL
- sp_replmonitorhelpmergesession
helpviewer_keywords:
- sp_replmonitorhelpmergesession
ms.assetid: a0400ba8-9609-4901-917e-925e119103a1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e08a08bbd3343386ed4b07749bde5216ae23c8b4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52789189"
---
# <a name="spreplmonitorhelpmergesession-transact-sql"></a>sp_replmonitorhelpmergesession (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回给定复制合并代理的以前会话的信息，并为每个符合筛选条件的会话返回一行。 此用于监视合并复制的存储过程在分发服务器的分发数据库上执行，或在订阅服务器的订阅数据库上执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replmonitorhelpmergesession [ [ @agent_name = ] 'agent_name' ]  
    [ , [ @hours = ] hours ]  
    [ , [ @session_type = ] session_type ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]   
```  
  
## <a name="arguments"></a>参数  
 [ **@agent_name** =] **'***agent_name*****  
 为代理的名称。 *agent_name*是**nvarchar(100)** ，无默认值。  
  
 [ **@hours** =]*小时*  
 以小时为单位的时间范围，将返回该范围内的历史代理会话信息。 *小时*是**int**，可以是下列范围之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|< **0**|返回代理过去运行的信息，最多返回 100 条运行信息。|  
|**0** （默认值）|返回代理过去运行的所有信息。|  
|> **0**|返回在代理上发生的运行中信息上次*小时*数小时。|  
  
 [ **@session_type** =] *session_type*  
 基于会话最终结果筛选结果集。 *session_type*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1** （默认值）|具有重试或成功结果的代理会话。|  
|**0**|具有失败结果的代理会话。|  
  
 [ **@publisher** = ] **'***publisher***'**  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。 执行时使用此参数**sp_replmonitorhelpmergesession**订阅服务器上。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 发布数据库的名称。 *publisher_db*是**sysname**，默认值为 NULL。 执行时使用此参数**sp_replmonitorhelpmergesession**订阅服务器上。  
  
 [ **@publication=** ] **'***发布*****  
 发布的名称。 *发布*是**sysname**，默认值为 NULL。 执行时使用此参数**sp_replmonitorhelpmergesession**订阅服务器上。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**Session_id**|**int**|代理作业会话的 ID。|  
|**“状态”**|**int**|代理运行状态：<br /><br /> **1** = 开始<br /><br /> **2** = 成功<br /><br /> **3** = 正在进行<br /><br /> **4** = 空闲<br /><br /> **5** = 重试<br /><br /> **6** = 失败|  
|**StartTime**|**datetime**|开始时间在代理作业会话。|  
|**EndTime**|**datetime**|时间在代理作业会话已完成。|  
|**Duration**|**int**|此作业会话的累计时间（以秒为单位）。|  
|**UploadedCommands**|**int**|在代理会话过程中上载的命令的数目。|  
|**DownloadedCommands**|**int**|在代理会话过程中下载的命令的数目。|  
|**ErrorMessages**|**int**|在代理会话过程中生成的错误消息的数目。|  
|**ErrorID**|**int**|发生的错误的 ID。|  
|**PercentageDone**|**decimal**|已经在活动会话中传递的全部更改的估计百分比。|  
|**TimeRemaining**|**int**|估计的活动会话所剩秒数。|  
|**CurrentPhase**|**int**|活动会话的当前阶段，可以是以下内容之一。<br /><br /> **1** = 上载<br /><br /> **2** = 下载|  
|**LastMessage**|**nvarchar(500)**|合并代理在会话过程中记录的最后一个消息。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_replmonitorhelpmergesession**用于监视合并复制。  
  
 在订阅服务器上执行时**sp_replmonitorhelpmergesession**只返回最后五个合并代理会话的信息。  
  
## <a name="permissions"></a>权限  
 只有的成员**db_owner**或**replmonitor**分发服务器上的分发数据库或订阅服务器上的订阅数据库上的固定的数据库角色可以执行**sp_replmonitorhelpmergesession**。  
  
## <a name="see-also"></a>请参阅  
 [以编程方式监视复制](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
