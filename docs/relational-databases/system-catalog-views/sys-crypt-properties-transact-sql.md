---
title: sys. crypt_properties （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- crypt_properties
- crypt_properties_TSQL
- sys.crypt_properties_TSQL
- sys.crypt_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.crypt_properties catalog view
ms.assetid: d5684f5a-30b1-418e-ae4d-ab040db9257e
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5a4c03687f6adac3f67f3e6aa231c384a6d5e009
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725803"
---
# <a name="syscrypt_properties-transact-sql"></a>sys.crypt_properties (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  对于与安全对象关联的每个加密属性，返回与其对应的一行。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|标识属性所在项的类。<br /><br /> 1 = 对象或列<br /> 5 = 程序集|  
|**class_desc**|**nvarchar(60)**|对于属性所在项的类的说明。<br /><br /> OBJECT_OR_COLUMN<br /> ASSEMBLY|  
|**major_id**|**int**|属性所在项的 ID，根据类解释。|  
|**指纹**|**varbinary(32)**|所用证书或非对称密钥的 SHA-1 哈希。|  
|**crypt_type**|**char （4）**|加密类型。<br /><br /> SPVC = 通过证书私钥签名<br /><br /> SPVA = 使用非对称私钥签名<br /><br /> CPVC = 使用证书私钥加密的计数器签名<br /><br /> CPVA = 使用非对称密钥加密的计数器签名|  
|**crypt_type_desc**|**nvarchar(60)**|对加密类型的说明。<br /><br /> SIGNATURE BY CERTIFICATE<br /><br /> SIGNATURE BY ASYMMETRIC KEY<br /><br /> COUNTER SIGNATURE BY CERTIFICATE<br /><br /> COUNTER SIGNATURE BY ASYMMETRIC KEY|  
|**crypt_property**|**varbinary(max)**|标记位或加密位。 对于已签名的模块，这些是模块的签名位。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;安全目录视图](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [安全对象](../../relational-databases/security/securables.md)   
 [CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)   
 [&#40;Transact-sql&#41;创建对称密钥](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [创建非对称密钥 &#40;Transact-sql&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
