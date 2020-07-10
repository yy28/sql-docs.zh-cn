---
title: sp_pdw_database_encryption_regenerate_system_keys (SQL 数据仓库) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: bb13e323-a984-4462-8b6d-6019c38ddd9d
author: ronortloff
ms.author: rortloff
ms.reviewer: ''
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 06ce871e8f67a9cf4fa57b81eb84f47161e8fd28
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197332"
---
# <a name="sp_pdw_database_encryption_regenerate_system_keys-sql-data-warehouse"></a>sp_pdw_database_encryption_regenerate_system_keys (SQL 数据仓库) 

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  使用**sp_pdw_database_encryption_regenerate_system_keys**轮换在设备上启用了 TDE 时加密的内部数据库的证书和数据库加密密钥。 这包括 `tempdb`。 仅当启用了 TDE 时，此功能才会成功。  
  
## <a name="syntax"></a>语法  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption_regenerate_system_keys  ;  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或**1** (失败)   
  
## <a name="remarks"></a>备注  
 此过程没有参数。  
  
 当设备中的流量较低时，应使用此过程。  
  
## <a name="permissions"></a>权限  
 要求具有**sysadmin**固定数据库角色的成员身份或**CONTROL SERVER**权限。  
  
## <a name="example"></a>示例  
 下面的示例重新生成数据库加密密钥。  
  
```sql  
EXEC sys.sp_pdw_database_encryption_regenerate_system_keys;  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_pdw_database_encryption &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
