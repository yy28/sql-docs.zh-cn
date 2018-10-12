---
title: 列加密 enclave 类型服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 961cf4a634f134f3bd41858a8157db0e8f6cb45f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782385"
---
# <a name="column-encryption-enclave-type-server-configuration-option"></a>列加密 enclave 类型服务器配置选项
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  使用“列加密 enclave 类型”选项来启用或禁用 Always Encrypted 的安全 enclave。  有关详细信息，请参阅[具有安全 enclave 的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。

 下表列出了可能的列加密 enclave 类型值：  
  
|ReplTest1|描述|  
|-------------------|-----------------|  
|0|没有安全 enclave。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不会为 Always Encrypted 初始化安全 enclave。 因此，具有安全 enclave 的 Always Encrypted 功能将不可用。|  
|1|基于虚拟化的安全性 (VBS)。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将为 Always Encrypted 初始化安全 enclave（VBS 安全内存 enclave）。|    

> [!IMPORTANT]
> 对列加密 enclave 类型的更改直到重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例才会生效。
  
   
## <a name="examples"></a>示例  
 以下示例启用安全 enclave：  

```sql  
sp_configure 'column encryption enclave type', 1;  
GO  
RECONFIGURE;  
GO  
```  

以下示例禁用安全 enclave：  

```sql  
sp_configure 'column encryption enclave type', 0;  
GO  
RECONFIGURE;  
GO  
```  

## <a name="see-also"></a>另请参阅  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
