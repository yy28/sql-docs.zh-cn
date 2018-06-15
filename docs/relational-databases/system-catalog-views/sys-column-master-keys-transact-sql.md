---
title: sys.column_master_keys (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- column_master_key_definitions_TSQL
- column_master_key_definitions
- sys.column_master_key_definitions_TSQL
- sys.column_master_key_definitions
- column_master_keys_TSQL
- column_master_keys
- sys.column_master_keys_TSQL
- sys.column_master_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_master_key_definitions catalog view
- sys.column_master_keys catalog view
ms.assetid: fbec2efa-5fe9-4121-9b34-60497b0b2aca
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7f961586da2bb4bd9a3169fe955d989557535ba7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33181773"
---
# <a name="syscolumnmasterkeys-transact-sql"></a>sys.column_master_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  为通过使用添加每个数据库主密钥返回一行[CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)语句。 每一行表示单个列主密钥 (CMK)。  
    
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|CMK 的名称。|  
|**column_master_key_id**|**int**|列主密钥 ID。|  
|**create_date**|**datetime**|列主密钥的创建日期。|  
|**modify_date**|**datetime**|上次修改列主密钥的日期。|  
|key_store_provider_name|**sysname**|包含 CMK 的列主密钥存储提供程序名称。 允许的值包括：<br /><br /> MSSQL_CERTIFICATE_STORE – 如果列主密钥存储为一个证书存储。<br /><br /> 用户定义的值，如果列主密钥存储的自定义的类型。|  
|**key_path**|**nvarchar(4000)**|列主密钥存储特定的密钥的路径。 路径的格式取决于列主密钥存储类型。 例如：<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> 对于自定义列主密钥存储，开发人员负责定义哪些项的路径为自定义列主密钥存储。|  
  
## <a name="permissions"></a>权限  
 需要**VIEW ANY COLUMN MASTER KEY**权限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Always Encrypted（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
