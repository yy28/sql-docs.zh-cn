---
title: MSpublications （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpublications
- MSpublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublications system table
ms.assetid: 7a0b3457-7265-4f24-a255-7f055d908f20
author: stevestein
ms.author: sstein
ms.openlocfilehash: de4970e82155454b3d05d6200bc7413baca97aef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67939014"
---
# <a name="mspublications-transact-sql"></a>MSpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  发布服务器复制的每个发布在**MSpublications**表中各占一行。 此表存储在分发数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|发布服务器的 ID。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**publication_id**|**int**|发布 ID。|  
|**publication_type**|**int**|发布类型：<br /><br /> **0** = 事务性。<br /><br /> **1** = 快照。<br /><br /> **2** = 合并。|  
|**thirdparty_flag**|**bit**|指示发布是否为[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库：<br /><br /> **** = 0[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br /> **1** = 之外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的数据源。|  
|**independent_agent**|**bit**|表明该发布是否有独立的分发代理。|  
|**immediate_sync**|**bit**|指示每次运行快照代理时是否创建或重新创建同步文件。|  
|**allow_push**|**bit**|指示是否可为给定发布创建推送订阅。|  
|**allow_pull**|**bit**|指示是否可为给定发布创建请求订阅。|  
|**allow_anonymous**|**bit**|指示是否可为给定发布创建匿名订阅。|  
|**2008**|**nvarchar(255)**|发布的说明。|  
|**vendor_name**|**nvarchar （100）**|供应商的名称（如果发布服务器不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库）。|  
|**保留**|**int**|发布的保持期（以小时为单位）。|  
|**sync_method**|**int**|同步方法包括：<br /><br /> **0** = 本机（生成所有表的本机模式大容量复制输出）。<br /><br /> **1** = 字符（生成所有表的字符模式大容量复制输出）。<br /><br /> **3** = 并发（生成所有表的本机模式大容量复制输出，但在快照过程中并不锁定表）。<br /><br /> **4** = Concurrent_c （生成所有表的字符模式大容量复制输出，但在快照过程中并不锁定表）<br /><br /> 值**3**和**4**可用于事务复制和合并复制，但不适用于快照复制。|  
|**allow_subscription_copy**|**bit**|启用或禁用对订阅此发布的订阅数据库的复制功能。 **0**表示禁用复制， **1**表示启用复制。|  
|**thirdparty_options**|**int**|指定是否禁止在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的复制文件夹中显示发布：<br /><br /> **0** = 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 Replication 文件夹中显示异类发布。<br /><br /> **1** = 禁止在的 Replication 文件夹中显示异类发布[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。|  
|**allow_queued_tran**|**bit**|指定发布是否允许排队更新：<br /><br /> **0 =** 发布未排队。<br /><br /> **1** = 发布已排队。|  
|**选项**|**int**|没有此版本的信息。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
