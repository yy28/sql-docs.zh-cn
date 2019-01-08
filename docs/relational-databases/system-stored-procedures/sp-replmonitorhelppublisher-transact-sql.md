---
title: sp_replmonitorhelppublisher (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublisher_TSQL
- sp_replmonitorhelppublisher
helpviewer_keywords:
- sp_replmonitorhelppublisher
ms.assetid: 171501fe-4b74-4647-96c3-7691c777e01b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5f8a7e698fcb4eeb0f1e10c00acf4c34d233f755
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52794909"
---
# <a name="spreplmonitorhelppublisher-transact-sql"></a>sp_replmonitorhelppublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为与分发服务器关联的一个或多个发布服务器返回当前状态信息。 在分发服务器的分发数据库上执行此存储过程，用于监视复制。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replmonitorhelppublisher [ [ @publisher = ] 'publisher' ]  
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher** = ] **'***publisher***'**  
 正监视其状态的发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。 如果为 NULL，则返回使用分发服务器的所有发布服务器的信息。  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 仅限内部使用。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|是发布服务器的名称。|  
|**distribution_db**|**sysname**|给定发布服务器使用的分发数据库的名称。|  
|**status**|**int**|与此发布服务器中的发布关联的所有复制代理的最大值状态，可以是下列值之一：<br /><br /> **1** = 开始<br /><br /> **2** = 成功<br /><br /> **3** = 正在进行<br /><br /> **4** = 空闲<br /><br /> **5** = 正在重试<br /><br /> **6** = 失败|  
|**警告**|**int**|由属于此发布服务器上的某发布的订阅生成的最大阈值警告，可以是以下一个或多个值的“逻辑或”结果。<br /><br /> **1** = 到期-在保留期阈值内尚未同步对事务发布的订阅。<br /><br /> **2** = latency-将数据从事务发布服务器复制到订阅服务器所用的时间超过阈值，以秒为单位。<br /><br /> **4** = mergeexpiration – 对合并发布的订阅尚未在保持期阈值内进行同步。<br /><br /> **8** = mergefastrunduration-完成的合并订阅同步所花费的时间超过阈值，以秒为单位，通过快速网络连接。<br /><br /> **16** = mergeslowrunduration-完成的合并订阅同步所花费的时间超过阈值，以秒为单位，通过慢速或拨号网络连接。<br /><br /> **32** = mergefastrunspeed-传送速率的行合并订阅的同步过程未能保持阈值速率，单位为每秒，行通过快速网络连接。<br /><br /> **64** = mergeslowrunspeed-传送速率的行合并订阅的同步过程未能保持阈值速率，单位为每秒，行通过慢速或拨号网络连接。|  
|**publicationcount**|**int**|属于发布服务器的发布的数量。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_replmonitorhelppublisher**用于所有类型的复制。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色的成员的分发服务器**db_owner**或**replmonitor**分发数据库中的固定的数据库角色可以执行**sp_replmonitorhelppublisher**。  
  
## <a name="see-also"></a>请参阅  
 [以编程方式监视复制](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
