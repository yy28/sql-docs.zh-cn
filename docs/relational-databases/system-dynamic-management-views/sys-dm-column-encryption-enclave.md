---
title: sys. dm_column_encryption_enclave (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: system-objects
ms.topic: language-reference
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: f41a5f704a50924a882e220786ac8cafc090237a
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279545"
---
# <a name="sysdm_column_encryption_enclave-transact-sql"></a>sys.dm_column_encryption_enclave (Transact-SQL)
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

返回 Always Encrypted 安全 enclave 的性能计数器。 有关详细信息，请参阅[具有安全 enclave 的 Always Encrypted](../security/encryption/always-encrypted-enclaves.md)。

如果已配置 enclave 并已在上一次重新启动后正确初始化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则该视图将只包含一行。 如果 enclave 未配置或未正确初始化，则视图不会返回任何行。 

|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|current_enclave_session_count|**int**|当前使用 enclave 的客户端会话数。|  
|current_column_encryption_key_count|**int**|Enclave 当前包含的列加密密钥的计数。|  
|current_memory_size_kb|**bigint**|Enclave 内存大小（KB）|  
|total_evicted_session_count|**bigint**|自上次服务器重新启动以来，enclave 会话的总计数。|   
  
## <a name="permissions"></a>权限  
需要 `VIEW SERVER STATE` 权限。   
  
## <a name="examples"></a>示例  
 
```sql  
SELECT * FROM sys.dm_column_encryption_enclave;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [配置 Always Encrypted 的 enclave 类型服务器配置选项](../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)
  
  
