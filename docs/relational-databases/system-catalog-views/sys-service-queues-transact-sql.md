---
title: sys.service_queues (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_queues
- service_queues
- service_queues_TSQL
- sys.service_queues_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_queues catalog view
ms.assetid: 9fd9fa76-6128-410c-896f-741e6050143a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 53e979acc65dcd700412e7d79237d5f6492bccba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078724"
---
# <a name="sysservicequeues-transact-sql"></a>sys.service_queues (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个对象与服务队列的数据库中存在对应的一行**sys.objects.type** = SQ。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**||此视图所继承的列的列表，请参阅[sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**max_readers**|**smallint**|队列中允许的并发读取器的最大数目。|  
|**activation_procedure**|**nvarchar(776)**|由三部分组成的激活过程名称。|  
|**execute_as_principal_id**|**int**|EXECUTE AS 数据库主体的 ID。<br /><br /> 默认情况下，或者 EXECUTE AS CALLER 时，为 NULL。<br /><br /> 指定主体 if 的 ID 执行 AS SELF EXECUTE AS\<主体 >。<br /><br /> -2 = EXECUTE AS OWNER。|  
|**is_activation_enabled**|**bit**|1 = 启用激活。|  
|**is_receive_enabled**|**bit**|1 = 启用接收。|  
|**is_enqueue_enabled**|**bit**|1 = 启用排入队列。|  
|**is_retention_enabled**|**bit**|1 = 保留消息直到对话结束。|  
|**is_poison_message_handling_enabled**|**bit**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = 启用有害消息处理。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
