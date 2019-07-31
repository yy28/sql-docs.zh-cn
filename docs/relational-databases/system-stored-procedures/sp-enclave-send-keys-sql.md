---
title: sp_enclave_send_keys (Transact-sql) |Microsoft Docs
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
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b4ced2feee2227ba1db492f721f57907069c5d99
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661352"
---
# <a name="spenclavesendkeys----transact-sql"></a>sp_enclave_send_keys    (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

将数据库中所有 enclave 启用的列加密密钥发送到[安全 enclaves &#40;数据库引擎&#41;Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)使用的 enclave。

## <a name="syntax"></a>语法  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>参数

此存储过程没有参数。

## <a name="return-value"></a>返回值

此存储过程没有返回值。
  
## <a name="result-sets"></a>结果集

此存储过程没有结果集。
  
## <a name="remarks"></a>备注

如果满足以下所有条件, 则**sp_enclave_send_keys**会将启用 enclave 的列加密密钥发送到 enclave:

- SQL Server 实例中启用了 enclave。
- 已使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端驱动程序从应用程序中调用 sp_enclave_send_keys, 支持使用具有 enclaves 和 enclave 计算的数据库 Always Encrypted 连接的安全 Always Encrypted。

## <a name="permissions"></a>权限

 需要**查看任意列加密密钥定义**, 并查看数据库中的**任何列主密钥定义**权限。  
  
## <a name="examples"></a>示例  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>请参阅

 [Always Encrypted 安全 enclaves &#40;数据库引擎&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [教程：使用随机加密为启用了 enclave 的列创建和使用索引](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md#step-3-create-an-index-with-role-separation)   
 [使用缓存的列加密密钥调用索引操作](../security/encryption/configure-always-encrypted-enclaves.md#invoke-indexing-operations-using-cached-column-encryption-keys)   
 [使用随机加密的启用 Enclave 的列上的索引](../security/encryption/always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)   
 [AlwaysOn 和数据库迁移注意事项](../security/encryption/always-encrypted-enclaves.md#anchorname-1-considerations-availability-groups-db-migration)
