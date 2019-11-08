---
title: 管理具有安全 enclave 的 Always Encrypted 的密钥 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d3968c5c8f04cba8581dfdd44ac847f7010de994
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595622"
---
# <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>管理具有安全 enclave 的 Always Encrypted 的密钥
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[具有安全 enclave 的 Always Encrypted](always-encrypted-enclaves.md) 通过引入已启用 enclave 的密钥来扩展 [Always Encrypted](always-encrypted-database-engine.md) 的密钥管理： 

- **已启用 enclave 的列主密钥** - 使用数据库内的列主密钥元数据对象中指定的 `ENCLAVE_COMPUTATIONS` 属性创建的列主密钥。 
- **已启用 enclave 的列加密密钥** – 使用已启用 enclave 的列主密钥加密的列加密密钥。 只有已启用 enclave 的列加密密钥才能用于服务器端安全 enclave 中的计算。 

[管理 Always Encrypted 密钥](overview-of-key-management-for-always-encrypted.md)的一般准则和流程适用于管理已启用 enclave 的密钥。 

## <a name="managing-keys"></a>管理密钥

以下文章介绍了管理已启用 enclave 的密钥的特定方面。

- [预配已启用 enclave 的密钥](always-encrypted-enclaves-provision-keys.md)
- [轮换已启用 enclave 的密钥](always-encrypted-enclaves-rotate-keys.md)

## <a name="next-steps"></a>Next Steps
- [预配已启用 enclave 的密钥](always-encrypted-enclaves-provision-keys.md)

## <a name="see-also"></a>另请参阅  
- [Always Encrypted 密钥管理概述](overview-of-key-management-for-always-encrypted.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
