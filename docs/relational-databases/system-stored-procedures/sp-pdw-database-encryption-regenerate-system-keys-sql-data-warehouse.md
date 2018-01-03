---
title: "sp_pdw_database_encryption_regenerate_system_keys （SQL 数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: bb13e323-a984-4462-8b6d-6019c38ddd9d
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad105aed33da4215bb40548a5b73cec6b6c9e8f7
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="sppdwdatabaseencryptionregeneratesystemkeys-sql-data-warehouse"></a>sp_pdw_database_encryption_regenerate_system_keys （SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  使用**sp_pdw_database_encryption_regenerate_system_keys**旋转时在设备上启用了 TDE 加密的内部数据库的证书和数据库加密密钥。 这包括 `tempdb`。 仅当启用了 TDE，这将会成功。  
  
## <a name="syntax"></a>语法  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption_regenerate_system_keys  ;  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 该过程没有任何参数。  
  
 在设备中的流量较低时，应使用此过程。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**sysadmin**固定数据库角色或**CONTROL SERVER**权限。  
  
## <a name="example"></a>示例  
 下面的示例将重新生成数据库加密密钥。  
  
```sql  
EXEC sys.sp_pdw_database_encryption_regenerate_system_keys;  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_pdw_database_encryption &#40;SQL 数据仓库 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL 数据仓库 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
