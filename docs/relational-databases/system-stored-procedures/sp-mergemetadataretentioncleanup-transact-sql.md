---
title: sp_mergemetadataretentioncleanup （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergemetadataretentioncleanup
- sp_mergemetadataretentioncleanup_TSQL
helpviewer_keywords:
- sp_mergemetadataretentioncleanup
ms.assetid: 4e8d6343-2a38-421d-a3f3-c37d437a0f88
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 78ef8690e4f8dd374125d4c8e6e77a4a1964d329
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828297"
---
# <a name="sp_mergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)、 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)、 [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)、 [MSmerge_past_partition_mappings](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)和[MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md)系统表中手动清除元数据。 此存储过程在每个发布服务器和订阅服务器的拓扑中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>参数  
`[ @num_genhistory_rows = ] num_genhistory_rows OUTPUT`返回从[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)表中清除的行数。 *num_genhistory_rows*的值为**int**，默认值为**0**。  
  
`[ @num_contents_rows = ] num_contents_rows OUTPUT`返回从[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)表中清除的行数。 *num_contents_rows*的值为**int**，默认值为**0**。  
  
`[ @num_tombstone_rows = ] num_tombstone_rows OUTPUT`返回从[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)表中清除的行数。 *num_tombstone_rows*的值为**int**，默认值为**0**。  
  
`[ @aggressive_cleanup_only = ] aggressive_cleanup_only`仅限内部使用。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
  
> [!IMPORTANT]  
>  如果数据库中有多个发布，并且其中任何一个发布使用无限发布保持期，则运行**sp_mergemetadataretentioncleanup**不会清理数据库的合并复制更改跟踪元数据。 因此，要谨慎使用无限发布保持。 若要确定发布是否具有无限**期的保留**期，请在发布服务器上执行[sp_helpmergepublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) ，并记下结果集中值为**0**的任何发布。  
  
## <a name="permissions"></a>权限  
 只有**db_owner**固定数据库角色的成员或已发布数据库的发布访问列表中的用户才能执行**sp_mergemetadataretentioncleanup**。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
