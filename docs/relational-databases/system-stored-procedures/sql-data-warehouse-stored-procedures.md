---
title: SQL 数据仓库存储的过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.service: sql-data-warehouse
ms.component: design
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02e04dfe-d565-4e45-b427-b8e89c958ba3
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: eb92907b87382c9aad2b7c1a580bf0feb33ac7bd
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51657146"
---
# <a name="sql-data-warehouse-stored-procedures"></a>SQL 数据仓库存储的过程
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 提供了可用于执行与数据库角色相关的操作的内置过程。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 包括下列系统过程：  
  
##  <a name="AggregateFunctions"></a> [sp_datatype_info_90 &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-datatype-info-90-sql-data-warehouse.md)  
  
 [sp_pdw_add_network_credentials &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
 [sp_pdw_log_user_data_masking &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
 [sp_pdw_remove_network_credentials &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
 [sp_special_columns_100 &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-special-columns-100-sql-data-warehouse.md)  
  
> [!NOTE]  
>  某些实例中仅使用存储的过程的其他系统[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或通过客户端 Api，不应为一般客户使用。 这些过程均列在[系统存储过程 (Transact SQL)](https://msdn.microsoft.com/library/ms187961.aspx)。 这些过程可能会有所变动，不保证兼容性。 在列表上的所有过程中都均不提供[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [系统存储函数&#40;Transact SQL&#41;](~/relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
