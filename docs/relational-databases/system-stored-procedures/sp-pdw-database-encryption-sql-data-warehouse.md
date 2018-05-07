---
title: sp_pdw_database_encryption （SQL 数据仓库） |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: da83081e3d5eb24a38424e6bdafc68014f6a490d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sppdwdatabaseencryption-sql-data-warehouse"></a>sp_pdw_database_encryption （SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  使用**sp_pdw_database_encryption**为上启用透明数据加密[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]设备。 当**sp_pdw_database_encryption**设置为 1，使用**ALTER DATABASE**语句以使用 TDE 加密数据库。  
  
## <a name="syntax"></a>语法  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  
  
#### <a name="parameters"></a>Parameters  
 [  **@enabled=** ]*启用*  
 确定是否启用透明数据加密。 *启用*是**int**，和可以是以下值之一：  
  
-   0 = 禁用  
  
-   1 = 启用  
  
 执行**sp_pdw_database_encryption**没有参数就是标量结果集装置上返回 TDE 的当前状态： 已禁用，0 或 1 表示启用。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 当使用启用 TDE **sp_pdw_database_encryption**，tempdb 数据库进行删除、 重新创建和加密。 为此，TDE 时不能启用在设备上使用 tempdb 其他活动会话。 启用或禁用设备上的 TDE 是设备的操作更改状态，在大多数情况下应执行一次中的设备生存期内，和在设备上没有流量时应执行。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**sysadmin**固定数据库角色或**CONTROL SERVER**权限。  
  
## <a name="example"></a>示例  
 下面的示例在设备上启用 TDE。  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
