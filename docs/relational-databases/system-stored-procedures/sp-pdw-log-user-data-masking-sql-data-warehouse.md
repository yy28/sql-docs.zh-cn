---
title: sp_pdw_log_user_data_masking （SQL 数据仓库） |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-data-warehouse
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 27b303f1e78826e74fb94f254a0c2e3692fbef7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sppdwloguserdatamasking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking （SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  使用**sp_pdw_log_user_data_masking**以启用用户数据中屏蔽[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动日志。 用户数据屏蔽会影响设备上的所有数据库的语句。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动日志受**sp_pdw_log_user_data_masking**确信[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动日志。 **sp_pdw_log_user_data_masking**不会影响数据库事务日志，或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]错误日志。  
  
 **背景信息：**在默认配置[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动日志包含完整[!INCLUDE[tsql](../../includes/tsql-md.md)]语句，并且在某些情况下可以包括如包含在操作中的用户数据**插入**， **更新**，和**选择**语句。 如果设备上的问题，这就允许分析导致了该问题并且无需重现此问题的条件。 为了防止用户数据都将写入到[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动日志，客户可以选择使用此存储的过程启用的用户数据屏蔽。 语句仍将写入[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动日志，但所有将屏蔽可能包含用户数据的语句中的文字; 替换为某些预定义的常量值。  
  
 在设备上启用透明数据加密时中的用户数据屏蔽[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动日志将自动打开。  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>Parameters  
 [ **@masking_mode=** ] *masking_mode*  
 确定是否启用透明数据加密日志用户数据屏蔽。 *masking_mode*是**int**，和可以是以下值之一：  
  
-   0 = 已禁用，用户数据将显示在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动日志。  
  
-   1 = 已启用，用户数据语句出现在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]屏蔽活动日志，但用户数据。  
  
-   2 = 的语句包含用户数据不会写入到[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动日志。  
  
 执行**sp_pdw_ log_user_data_masking**没有参数就是标量结果集装置上返回 TDE 日志用户数据屏蔽的当前状态。  
  
## <a name="remarks"></a>注释  
 用户数据在掩蔽[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动中的预定义常量值使用记录的文本启用替换**选择**和 DML 语句，因为它们可以包含用户数据。 设置*masking_mode*为 1 不会屏蔽元数据，例如列名称或表名称。 设置*masking_mode*为 2 中删除与元数据，例如列名称或表名称的语句。  
  
 用户数据在掩蔽[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动日志实现方式如下：  
  
-   TDE 和用户数据在掩蔽[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]默认关闭活动日志。 语句将不自动屏蔽，如果设备上未启用数据库加密。  
  
-   在设备上启用 TDE 将自动开启中的用户数据屏蔽[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动日志。  
  
-   禁用 TDE 不会影响用户数据在掩蔽[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活动日志。  
  
-   你可以显式启用用户数据在掩蔽[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]通过使用活动日志**sp_pdw_log_user_data_masking**过程。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**sysadmin**固定数据库角色或**CONTROL SERVER**权限。  
  
## <a name="example"></a>示例  
 以下示例启用 TDE 日志用户数据屏蔽在设备上。  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_pdw_database_encryption &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
