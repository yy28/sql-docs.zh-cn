---
title: 系统dm_database_encryption_keys（转算-SQL） |微软文档
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_database_encryption_keys
- sys.dm_database_encryption_keys_TSQL
- dm_database_encryption_keys
- dm_database_encryption_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_database_encryption_keys dynamic management view
ms.assetid: 56fee8f3-06eb-4fff-969e-abeaa0c4b8e4
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6e716c826fd366fda4505b7fcf9ec8e3b756ec25
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531053"
---
# <a name="sysdm_database_encryption_keys-transact-sql"></a>sys.dm_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回与数据库加密状态以及相关联数据库加密密钥有关的信息。 有关数据库加密的详细信息，请参阅[透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)。  
 
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|database_id|**Int**|数据库 ID。|  
|encryption_state|**Int**|指示数据库是加密的还是未加密的。<br /><br /> 0 = 不存在数据库加密密钥，未加密<br /><br /> 1 = 未加密<br /><br /> 2 = 正在进行加密<br /><br /> 3 = 已加密<br /><br /> 4 = 正在更改密钥<br /><br /> 5 = 正在进行解密<br /><br /> 6 = 正在进行保护更改（正在更改对数据库加密密钥进行加密的证书或非对称密钥）。|  
|create_date|**datetime**|显示创建加密密钥的日期（以 UTC 表示）。|  
|regenerate_date|**datetime**|显示重新生成加密密钥的日期（以 UTC 表示）。|  
|modify_date|**datetime**|显示已修改加密密钥的日期（以 UTC 表示）。|  
|set_date|**datetime**|显示加密密钥应用于数据库的日期（以 UTC 表示）。|  
|opened_date|**datetime**|显示上次打开数据库密钥时（以 UTC 表示）。|  
|key_algorithm|**nvarchar(32)**|显示用于密钥的算法。|  
|key_length|**Int**|显示密钥的长度。|  
|encryptor_thumbprint|**varbinary(20)**|显示加密程序的指纹。|  
|encryptor_type|**nvarchar(32)**|**应用于**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] （通过[当前版本](https://go.microsoft.com/fwlink/p/?LinkId=299658)）。<br /><br /> 描述加密程序。|  
|percent_complete|**真正**|数据库加密状态更改的完成百分比。 如果未发生状态更改，则为 0。|
|encryption_state_desc|**nvarchar(32)**|**适用于**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]及更高版本。<br><br> 指示数据库是否加密的字符串。<br><br>无<br><br>加密<br><br>加密<br><br>DECRYPTION_IN_PROGRESS<br><br>ENCRYPTION_IN_PROGRESS<br><br>KEY_CHANGE_IN_PROGRESS<br><br>PROTECTION_CHANGE_IN_PROGRESS|
|encryption_scan_state|**Int**|**适用于**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]及更高版本。<br><br>指示加密扫描的当前状态。 <br><br>0 = 未启动扫描，未启用 TDE<br><br>1 = 扫描正在进行中。<br><br>2 = 扫描正在进行中，但已暂停，用户可以继续。<br><br>3 = 扫描由于某种原因中止，需要手动干预。 请与微软支持部门联系以获得更多帮助。<br><br>4 = 扫描已成功完成，TDE 已启用，加密已完成。|
|encryption_scan_state_desc|**nvarchar(32)**|**适用于**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]及更高版本。<br><br>指示加密扫描的当前状态的字符串。<br><br> 无<br><br>RUNNING<br><br>SUSPENDED<br><br>ABORTED<br><br>完成|
|encryption_scan_modify_date|**datetime**|**适用于**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]及更高版本。<br><br> 显示上次修改的加密扫描状态的日期（以 UTC 表示）。|
  
## <a name="permissions"></a>权限

打开[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]时`VIEW SERVER STATE`，需要权限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层上，需要数据库中`VIEW DATABASE STATE`的权限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准和基本层上，需要**服务器管理员**或 Azure**活动目录管理员**帐户。   

## <a name="see-also"></a>另请参阅  

 [与安全相关的动态管理视图和功能&#40;处理-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [透明数据加密&#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL 服务器加密](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL 服务器和数据库加密密钥&#40;数据库引擎&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [更改数据库集选项&#40;转算-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [创建数据库加密密钥&#40;交易-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [更改数据库加密密钥&#40;转算-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY (Transact-SQL)](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  
