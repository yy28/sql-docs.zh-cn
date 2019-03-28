---
title: sp_pdw_database_encryption （SQL 数据仓库） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a2ab88ca9a65d65e80f715ff4f8eb13c31b2d903
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536399"
---
# <a name="sppdwdatabaseencryption-sql-data-warehouse"></a>sp_pdw_database_encryption （SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  使用**sp_pdw_database_encryption**上启用透明数据加密的[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]设备。 当**sp_pdw_database_encryption**设置为 1，使用**ALTER DATABASE**语句以使用 TDE 加密数据库。  
  
## <a name="syntax"></a>语法  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  
  
#### <a name="parameters"></a>Parameters  
`[ @enabled = ] enabled` 确定是否启用透明数据加密。 *已启用*是**int**，可以是下列值之一：  
  
-   0 = 禁用  
  
-   1 = 启用  
  
 执行**sp_pdw_database_encryption**没有参数作为标量结果集在设备上返回 TDE 的当前状态：启用已禁用，为 0 或 1。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 如果使用启用 TDE **sp_pdw_database_encryption**，删除、 重新创建并加密 tempdb 数据库。 出于此原因，不能是上启用 TDE 一台设备使用 tempdb 其他活动会话时。 启用或禁用设备上的 TDE 是设备，在大多数情况下的状态更改的操作应执行一次在设备生命周期，和在设备上没有流量时应执行。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**sysadmin**固定数据库角色或**CONTROL SERVER**权限。  
  
## <a name="example"></a>示例  
 下面的示例在设备上启用 TDE。  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
