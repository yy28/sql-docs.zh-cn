---
title: MSpublications (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSpublications
- MSpublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublications system table
ms.assetid: 7a0b3457-7265-4f24-a255-7f055d908f20
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ab3987fddb89b3ec037d191be0d640922675428e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="mspublications-transact-sql"></a>MSpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpublications**表包含个通过发布服务器复制每个发布都占一行。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**int**|发布服务器的 ID。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**publication_id**|**int**|发布 ID。|  
|**publication_type**|**int**|发布类型：<br /><br /> **0** = 事务。<br /><br /> **1** = 快照。<br /><br /> **2** = 合并。|  
|**thirdparty_flag**|**bit**|该值指示是否发布[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库：<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **1**以外 = 数据源[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**independent_agent**|**bit**|表明该发布是否有独立的分发代理。|  
|**immediate_sync**|**bit**|指示每次运行快照代理时是否创建或重新创建同步文件。|  
|**allow_push**|**bit**|指示是否可以为给定的发布创建推送订阅。|  
|**allow_pull**|**bit**|指示是否可为给定发布创建请求订阅。|  
|**allow_anonymous**|**bit**|指示是否可以为给定的发布创建匿名订阅。|  
|**说明**|**nvarchar(255)**|发布的说明。|  
|**vendor_name**|**nvarchar(100)**|供应商的名称（如果发布服务器不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库）。|  
|**保持期**|**int**|发布的保持期（以小时为单位）。|  
|**sync_method**|**int**|同步方法包括：<br /><br /> **0** = 的 native （生成的所有表的纯模式大容量复制输出）。<br /><br /> **1** = 的字符 （生成的所有表的字符模式大容量复制输出）。<br /><br /> **3** = 并发 （生成的所有纯模式大容量复制输出表，但不会在快照期间锁定表）。<br /><br /> **4** = Concurrent_c （生成的所有字符模式大容量复制输出表，但不会在快照期间锁定表）<br /><br /> 值**3**和**4**提供有关事务复制和合并复制，而不是快照复制。|  
|**allow_subscription_copy**|**bit**|启用或禁用对订阅此发布的订阅数据库的复制功能。 **0**意味着禁用了复制，和**1**意味着启用它。|  
|**thirdparty_options**|**int**|指定是否在复制文件夹中的发布显示[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]取消：<br /><br /> **0** = 显示在复制文件夹中的异类发布[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。<br /><br /> **1** = 禁止显示中的复制文件夹中的异类发布[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。|  
|**allow_queued_tran**|**bit**|指定发布是否允许排队更新：<br /><br /> **0 =** 发布是非排队。<br /><br /> **1** = 排队发布。|  
|**options**|**int**|没有此版本的信息。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
