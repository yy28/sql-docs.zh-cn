---
title: sys. sys.openkeys （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- openkeys_TSQL
- sys.openkeys_TSQL
- openkeys
- sys.openkeys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.openkeys catalog view
ms.assetid: 719a1259-2398-4fcb-ba05-aeabba7aec21
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e23d8c1453211592f5d6ff0de70db081de1fbb29
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760313"
---
# <a name="sysopenkeys-transact-sql"></a>sys.openkeys (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  此目录视图可返回有关当前对话中打开的加密密钥的信息。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|包含密钥的数据库的 ID。|  
|**database_name**|**sysname**|包含密钥的数据库的名称。|  
|**key_id**|**int**|密钥的 ID。 该 ID 在数据库中是唯一的。|  
|**key_name**|**sysname**|密钥的名称。 在数据库中是唯一的。|  
|**key_guid**|**varbinary**|密钥的 GUID。 在数据库中是唯一的。|  
|**opened_date**|**datetime**|打开密钥的日期和时间。|  
|**status**|**int**|如果密钥在元数据中有效，则为 1。 如果在元数据中找不到密钥，则为 0。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [OPEN SYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/open-symmetric-key-transact-sql.md)  
  
  
