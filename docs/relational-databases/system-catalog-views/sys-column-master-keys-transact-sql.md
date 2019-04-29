---
title: sys.column_master_keys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1cb1740bdb0ae26d91e2a9ad9e2becb69d3b2810
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013715"
---
# <a name="syscolumnmasterkeys-transact-sql"></a>sys.column_master_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  返回为每个数据库主密钥，使用添加一行[CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)语句。 每行代表单个列主密钥 (CMK)。  
    
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|CMK 的名称。|  
|**column_master_key_id**|**int**|列主密钥的 ID。|  
|**create_date**|**datetime**|创建列主密钥的日期。|  
|**modify_date**|**datetime**|列主密钥的上次修改日期。|  
|key_store_provider_name|**sysname**|包含 CMK 列主密钥存储提供程序的名称。 允许的值包括：<br /><br /> MSSQL_CERTIFICATE_STORE-如果列主密钥存储为证书存储区。<br /><br /> 用户定义的值，如果列主密钥存储的自定义类型。|  
|**key_path**|**nvarchar(4000)**|键的列主密钥存储特定于的路径。 路径的格式取决于列主密钥存储类型。 例如：<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> 对于自定义列主密钥存储，开发人员负责定义哪些项的路径为自定义列主密钥存储。|  
|**allow_enclave_computations**|**bit**|指示列主密钥是否已启用 enclave 的 （如果使用此主密钥加密的列加密密钥可用于在服务器端安全 enclaves 计算）。 有关详细信息，请参阅[具有安全 enclave 的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。|  
|signature|**varbinary(max)**|数字签名的**key_path**并**allow_enclave_computations**，生成使用列主密钥，引用**key_path**。|


  
## <a name="permissions"></a>权限  
 需要**VIEW ANY COLUMN MASTER KEY**权限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Always Encrypted（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
