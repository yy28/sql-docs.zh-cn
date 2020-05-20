---
title: sys. dm_cryptographic_provider_algorithms （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cryptographic_provider_algorithms_TSQL
- sys.dm_cryptographic_provider_algorithms
- sys.dm_cryptographic_provider_algorithms_TSQL
- dm_cryptographic_provider_algorithms
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_algorithms dynamic management function
ms.assetid: 8bcccb37-5cfb-4e1e-a0bb-7ff4c279fe8e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d465515d6446c16fc9186b03eafc9a287571bc5e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824670"
---
# <a name="sysdm_cryptographic_provider_algorithms-transact-sql"></a>sys.dm_cryptographic_provider_algorithms (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回可扩展密钥管理（EKM）提供程序支持的算法。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.dm_cryptographic_provider_algorithms ( provider_id )  
```  
  
## <a name="arguments"></a>参数  
 *provider_id*  
 EKM 提供程序的标识号，没有默认值。  
  
## <a name="tables-returned"></a>返回的表  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|algorithm_id|**int**|算法的标识号。|  
|algorithm_tag|**nvarchar(60)**|算法的标识标记。|  
|key_type|**nvarchar(128)**|显示密钥类型。 返回 ASYMMETRIC KEY 或 SYMMETRIC KEY。|  
|key_length|**int**|指示密钥长度（以位为单位）。|  
  
## <a name="permissions"></a>权限  
 用户必须是公用数据库角色的成员。  
  
## <a name="examples"></a>示例  
 下面的示例显示了标识号为 `1234567` 的提供程序的提供程序选项。  
  
```  
SELECT * FROM sys.dm_cryptographic_provider_algorithms(1234567);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [可扩展的密钥管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [与安全性相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
