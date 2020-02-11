---
title: sys. service_contract_message_usages （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- service_contract_message_usages_TSQL
- sys.service_contract_message_usages
- sys.service_contract_message_usages_TSQL
- service_contract_message_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_contract_message_usages catalog view
ms.assetid: f783e662-126c-4595-8e22-f9d05191f5d0
author: stevestein
ms.author: sstein
ms.openlocfilehash: bca839c61a59c69a7f6cf7e659ad940864fcee37
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132934"
---
# <a name="sysservice_contract_message_usages-transact-sql"></a>sys.service_contract_message_usages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在此目录视图中，每个（约定、消息类型）对对应一行。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**service_contract_id**|**int**|使用消息类型的约定的标识符。 不可为 NULL。|  
|**message_type_id**|**int**|约定所使用的消息类型的标识符。 不可为 NULL。|  
|**is_sent_by_initiator**|**bit**|可由会话发起方发送消息类型。 不可为 NULL。|  
|**is_sent_by_target**|**bit**|可由会话目标发送消息类型。 不可为 NULL。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
