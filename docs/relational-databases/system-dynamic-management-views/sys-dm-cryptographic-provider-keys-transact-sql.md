---
title: sys.dm_cryptographic_provider_keys (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
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
- sys.dm_cryptographic_provider_keys_TSQL
- dm_cryptographic_provider_keys_TSQL
- dm_cryptographic_provider_keys
- sys.dm_cryptographic_provider_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_keys dynamic management function
ms.assetid: 5a8c1421-c56b-44b5-96e5-4f01782a0c7c
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 285568b8953330a3cf28e06507b154a7397c9826
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmcryptographicproviderkeys-transact-sql"></a>sys.dm_cryptographic_provider_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关可扩展密钥管理 (EKM) 提供程序提供的密钥的信息。  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
dm_cryptographic_provider_keys ( provider_id )  
```  
  
## <a name="arguments"></a>参数  
 *provider_id*  
 EKM 提供程序的标识号，没有默认值。  
  
## <a name="tables-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**key_id**|**int**|提供程序中密钥的标识号。|  
|**key_name**|**nvarchar(512)**|提供程序中密钥的名称。|  
|**key_thumbprint**|**varbinary(32)**|来自密钥提供程序的指纹。|  
|**algorithm_id**|**int**|提供程序中算法的标识号。|  
|**algorithm_tag**|**int**|提供程序中算法的标记。|  
|**key_type**|**nchar(256)**|提供程序中密钥的类型。|  
|**key_length**|**int**|提供程序中密钥的长度。|  
  
## <a name="permissions"></a>权限  
 查询此视图时，它会将用户上下文送至提供程序进行身份验证并枚举用户可见的所有密钥。  
  
 如果用户无法通过 EKM 提供程序的身份验证，则不会返回任何密钥信息。  
  
## <a name="examples"></a>示例  
 下面的示例显示了标识号为 `1234567` 的提供程序的密钥属性。  
  
```  
SELECT * FROM sys.dm_cryptographic_provider_keys(1234567);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [可扩展密钥管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
