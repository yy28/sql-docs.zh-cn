---
title: sys. dm_cryptographic_provider_sessions （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cryptographic_provider_sessions
- dm_cryptographic_provider_sessions_TSQL
- sys.dm_cryptographic_provider_sessions_TSQL
- dm_cryptographic_provider_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_sessions dynamic management function
ms.assetid: 9a4de02b-1a07-4850-979a-0861fddb7f9d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 852566e9f337536717273c18b8034f3854fd7d48
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85894560"
---
# <a name="sysdm_cryptographic_provider_sessions-transact-sql"></a>sys.dm_cryptographic_provider_sessions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  返回有关加密提供程序的已打开会话的信息。  
 
## <a name="syntax"></a>语法  
  
```  
  
sys.dm_cryptographic_provider_sessions(session_identifier)  
```  
  
## <a name="arguments"></a>参数  
 *session_identifier*  
 指示要返回的会话的整数。  
  
 0 = 仅限当前连接  
  
 1 = 所有加密连接  
  
## <a name="table-returned"></a>返回的表  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**provider_id**|**int**|加密提供程序的标识号。|  
|**session_handle**|**varbytes （8）**|加密会话句柄。|  
|**identity**|**nvarchar(128)**|用于送至加密提供程序进行身份验证的标识。|  
|**spid**|**short**|连接的会话 ID SPID。 有关详细信息，请参阅 [@@SPID (Transact-SQL)](../../t-sql/functions/spid-transact-sql.md)。|  
  
## <a name="remarks"></a>备注  
 **Sys. dm_cryptographic_provider_sessions**视图对当前连接的 public 可见。 若要查看所有加密连接，必须具有**CONTROL** server 权限。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;安全目录视图](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [可扩展的密钥管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [&#40;Transact-sql&#41;创建加密提供程序](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
