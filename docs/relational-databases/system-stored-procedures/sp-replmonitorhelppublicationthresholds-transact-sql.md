---
title: sp_replmonitorhelppublicationthresholds (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublicationthresholds
- sp_replmonitorhelppublicationthresholds_TSQL
helpviewer_keywords:
- sp_replmonitorhelppublicationthresholds
ms.assetid: d6b1aa4b-3369-4255-a892-c0e5cc9cb693
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b9e2ecc46c668f8c9cb3bd8d9a2fb21d0c9787a6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47803205"
---
# <a name="spreplmonitorhelppublicationthresholds-transact-sql"></a>sp_replmonitorhelppublicationthresholds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回为所监视发布设置的阈值度量指标。 在分发服务器的分发数据库上执行此存储过程，用于监视复制。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replmonitorhelppublicationthresholds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'  
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher**=] **'***发布服务器***’**  
 发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [ **@publisher_db**=] **'***publisher_db***’**  
 已发布数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@publication**=] **'***发布***’**  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@publication_type**=] *publication_type*  
 发布的类型。 *publication_type*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|事务发布。|  
|**1**|快照发布。|  
|**2**|合并发布。|  
|NULL（默认值）|由复制来确定发布类型。|  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|复制性能度量指标的 ID，可为下列值之一。<br /><br /> **1expiration** -监视对事务发布的订阅是否即将过期。<br /><br /> **2latency** -监视对事务发布的订阅的性能。<br /><br /> **4mergeexpiration** -合并发布的订阅是否即将过期的监视器。<br /><br /> **5mergeslowrunduration** -监视通过低带宽 （拨号） 连接的合并同步的持续时间。<br /><br /> **6mergefastrunduration** -监视通过高带宽 (LAN) 连接的合并同步的持续时间。<br /><br /> **7mergefastrunspeed** -监视通过高带宽 (LAN) 连接的合并同步的同步速率。<br /><br /> **8mergeslowrunspeed** -监视通过低带宽 （拨号） 连接的合并同步的同步速率。|  
|**title**|**sysname**|复制性能度量指标的名称。|  
|**value**|**int**|性能度量指标的阈值。|  
|**shouldalert**|**bit**|当指标超过为此发布; 定义的阈值时应生成警报值为**1**指示应引发警报。|  
|**isenabled**|**bit**|如果为此发布; 此复制性能跃点启用了监视值为**1**指示启用监视。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_replmonitorhelppublicationthresholds**用于所有类型的复制。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**db_owner**或**replmonitor**固定的数据库角色的分发数据库才能执行**sp_replmonitorhelppublicationthresholds**。  
  
## <a name="see-also"></a>请参阅  
 [以编程方式监视复制](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
