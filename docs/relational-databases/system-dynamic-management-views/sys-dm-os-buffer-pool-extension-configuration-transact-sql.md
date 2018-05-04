---
title: sys.dm_os_buffer_pool_extension_configuration (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_buffer_pool_extension_configuration
- sys.dm_os_buffer_pool_extension_configuration_TSQL
- dm_os_buffer_pool_extension_configuration_TSQL
- sys.dm_os_buffer_pool_extension_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_buffer_pool_extension_configuration dynamic management view
ms.assetid: d52cc481-4d29-4f33-b63d-231ec35d092f
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 261c2217b91997262ae8951fce732e59bd2d55a2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmosbufferpoolextensionconfiguration-transact-sql"></a>sys.dm_os_buffer_pool_extension_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中有关缓冲池扩展的配置信息。 对每个缓冲池扩展文件返回一行。  
  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|path|**nvarchar**(256)|缓冲池扩展缓存的路径和文件名。 可以为 NULL。|  
|file_id|**int**|缓冲池扩展文件的 ID。 不可为 null。|  
|state|**int**|缓冲池扩展功能的状态。 不可为 null。<br /><br /> 0 - 已禁用缓冲池扩展<br /><br /> 1 - 正在禁用缓冲池扩展<br /><br /> 2-保留供将来使用<br /><br /> 3 - 正在启用缓冲池扩展<br /><br /> 4 - 保留以供将来使用<br /><br /> 5 - 已启用缓冲池扩展|  
|state_description|**nvarchar**(60)|说明缓冲池扩展功能的状态。 可以为 Null。<br /><br /> 0 = BUFFER POOL EXTENSION DISABLED<br /><br /> 1 = BUFFER POOL EXTENSION ENABLED|  
|current_size_in_kb|**bigint**|缓冲池扩展文件的当前大小。 不可为 null。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-configuration-buffer-pool-extension-information"></a>A. 返回配置缓冲池扩展信息  
 下面的示例从 sys.dm_os_buffer_pool_extension_configruation DMV 返回所有列。  
  
```sql  
SELECT path, file_id, state, state_description, current_size_in_kb  
FROM sys.dm_os_buffer_pool_extension_configuration;  
```  
  
### <a name="b-returning-the-number-of-cached-pages-in-the-buffer-pool-extension-file"></a>B. 返回缓冲池扩展文件中的缓存页数。  
 下面的示例返回每个缓冲池扩展文件中的缓存页数。  
  
```sql  
SELECT COUNT(*) AS cached_pages_count  
FROM sys.dm_os_buffer_descriptors  
WHERE is_in_bpool_extension <> 0  
;  
```  
  
## <a name="see-also"></a>另请参阅  
 [缓冲池扩展](../../database-engine/configure-windows/buffer-pool-extension.md)   
 [sys.dm_os_buffer_descriptors & #40;Transact SQL & #41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)  
  
  
