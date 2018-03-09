---
title: "sys.linked_logins (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.linked_logins
- sys.linked_logins_TSQL
- linked_logins_TSQL
- linked_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.linked_logins catalog view
ms.assetid: af57bf0c-a265-410f-9bab-63b78569b4a6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ca2137294edf7a24c0ad5b167c5e1037a86cab1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="syslinkedlogins-transact-sql"></a>sys.linked_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为每个链接服务器登录映射返回一行，供 RPC 以及从本地服务器到相应的链接服务器的分布式查询使用。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|中的服务器 ID **sys.servers**。|  
|**local_principal_id**|**int**|对其应用映射的服务器主体。<br /><br /> 0 = 通配符或公共主体。|  
|**uses_self_credential**|**bit**|如果为 1，则映射表示会话应使用它自己的凭据；否则为 0，表示会话使用提供的名称和密码。|  
|**remote_name**|**sysname**|连接时使用的远程用户名。 虽然也存储了密码，但并不显示在目录视图界面中。|  
|**modify_date**|**datetime**|上次更改该链接登录名的日期。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [链接的服务器目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)  
  
  
