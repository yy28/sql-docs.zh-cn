---
title: SQL 数据仓库存储过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.service: sql-data-warehouse
ms.subservice: design
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02e04dfe-d565-4e45-b427-b8e89c958ba3
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7aa82ee5c5a617c3564ac9246f2e42bebcab220e
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844355"
---
# <a name="sql-data-warehouse-stored-procedures"></a>SQL 数据仓库存储过程
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 提供了可用于执行与数据库角色相关的操作的内置过程。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 包括以下系统过程：  
  
##  <a name="AggregateFunctions"></a>[sp_datatype_info_90 &#40;SQL 数据仓库&#41; ](../../relational-databases/system-stored-procedures/sp-datatype-info-90-sql-data-warehouse.md)  
  
 [sp_pdw_add_network_credentials &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
 [sp_pdw_log_user_data_masking &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
 [sp_pdw_remove_network_credentials &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
 [sp_special_columns_100 &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-special-columns-100-sql-data-warehouse.md)  
  
> [!NOTE]  
>  一些其他系统存储过程只能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例中使用，也不能在客户端 Api 中使用，并且不适合一般客户使用。 [系统存储过程（transact-sql）](https://msdn.microsoft.com/library/ms187961.aspx)中列出了这些过程。 这些过程可能会发生更改，并且不保证兼容性。 列表中的所有过程在 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]中都不可用。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储函数&#40;transact-sql&#41; ](~/relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
