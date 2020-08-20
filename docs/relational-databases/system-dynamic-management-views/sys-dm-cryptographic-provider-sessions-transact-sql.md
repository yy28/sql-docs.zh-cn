---
description: sys.dm_cryptographic_provider_sessions (Transact-SQL)
title: sys. dm_cryptographic_provider_sessions (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 37a8854da08439c4dc3984bcdfc61a8695467c2b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455007"
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
|**session_handle**|**varbytes (8) **|加密会话句柄。|  
|**identity**|**nvarchar(128)**|用于送至加密提供程序进行身份验证的标识。|  
|spid|**short**|连接的会话 ID SPID。 有关详细信息，请参阅 [@@SPID (Transact-SQL)](../../t-sql/functions/spid-transact-sql.md)。|  
  
## <a name="remarks"></a>备注  
 **Sys. dm_cryptographic_provider_sessions**视图对当前连接的 public 可见。 若要查看所有加密连接，必须具有 **CONTROL** server 权限。  
  
## <a name="see-also"></a>另请参阅  
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [可扩展密钥管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
