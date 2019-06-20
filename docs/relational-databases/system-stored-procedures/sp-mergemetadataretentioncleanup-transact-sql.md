---
title: sp_mergemetadataretentioncleanup (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1797200ce5369f49035f1a950d606e34e584edc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62658414"
---
# <a name="spmergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  中的元数据中手动清除[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)， [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)， [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)， [MSmerge_past_partition_映射](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)，并[MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md)系统表。 此存储过程在每个发布服务器和订阅服务器的拓扑中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>参数  
`[ @num_genhistory_rows = ] num_genhistory_rows OUTPUT` 返回的行清除从数[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)表。 *num_genhistory_rows*是**int**，默认值为**0**。  
  
`[ @num_contents_rows = ] num_contents_rows OUTPUT` 返回的行清除从数[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)表。 *num_contents_rows*是**int**，默认值为**0**。  
  
`[ @num_tombstone_rows = ] num_tombstone_rows OUTPUT` 返回的行清除从数[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)表。 *num_tombstone_rows*是**int**，默认值为**0**。  
  
`[ @aggressive_cleanup_only = ] aggressive_cleanup_only` 仅限内部使用。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
  
> [!IMPORTANT]  
>  如果有多个发布数据库，并且任何一个发布使用无限发布保持期，请运行**sp_mergemetadataretentioncleanup**不会清除合并复制更改跟踪数据库的元数据。 因此，要谨慎使用无限发布保持。 若要确定发布是否具有无限保持期，请执行[sp_helpmergepublication &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)在发布服务器并记下结果中的任何发布设置的值为**0**有关**保留**。  
  
## <a name="permissions"></a>权限  
 只有的成员**db_owner**固定数据库角色或发布访问列表中的用户已发布的数据库才能执行**sp_mergemetadataretentioncleanup**。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
