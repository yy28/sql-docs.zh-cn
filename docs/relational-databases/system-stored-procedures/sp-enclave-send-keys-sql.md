---
title: sp_enclave_send_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_enclave_send_keys
- sp_enclave_send_keys_TSQL
- sys.sp_enclave_send_keys
- sys.sp_enclave_send_keys_TSQL
helpviewer_keywords:
- sp_enclave_send_keys
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6540cdd36cccba4f5a7ccb3beddf31ce00cd9107
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394139"
---
# <a name="spenclavesendkeys----transact-sql"></a>sp_enclave_send_keys    (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

将发送所有已启用 enclave 的列加密密钥在数据库中到使用的 enclave [Always Encrypted 与安全 enclaves&#40;数据库引擎&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。

## <a name="syntax"></a>语法  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>参数

此存储的过程有任何自变量。

## <a name="return-value"></a>返回值

此存储的过程有没有返回值。
  
## <a name="result-sets"></a>结果集

此存储的过程有任何结果集。
  
## <a name="remarks"></a>备注

**sp_enclave_send_keys**发送至 enclave 的已启用 enclave 的列加密密钥，如果满足所有以下条件：

- 中的 SQL Server 实例启用了 enclave。
- **sp_enclave_send_keys**已从应用程序中使用调用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端驱动程序，与使用具有始终加密并 enclave 计算已启用的数据库连接的安全 enclaves 支持始终加密。

## <a name="permissions"></a>权限

 需要**查看任意列加密密钥定义**并**查看任意列主密钥定义**数据库中的权限。  
  
## <a name="examples"></a>示例  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>另请参阅

 [使用安全 enclaves 始终加密&#40;数据库引擎&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [教程：创建和使用随机的加密已启用 enclave 的列上使用索引](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md#step-3-create-an-index-with-role-separation)   
 [调用索引操作使用缓存的列加密密钥](../security/encryption/configure-always-encrypted-enclaves.md#invoke-indexing-operations-using-cached-column-encryption-keys)   
 [使用随机加密已启用 Enclave 的列的索引](../security/encryption/always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)   
 [AlwaysOn 和数据库迁移注意事项](../security/encryption/always-encrypted-enclaves.md#considerations-for-alwayson-and-database-migration)
