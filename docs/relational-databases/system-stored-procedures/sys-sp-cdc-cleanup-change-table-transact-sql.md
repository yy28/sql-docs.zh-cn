---
title: "sys.sp_cdc_cleanup_change_table (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cdc_cleanup_change_table
- sp_cdc_cleanup_change_table_TSQL
- sys.sp_cdc_cleanup_change_table
- sys.sp_cdc_cleanup_change_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_cleanup_change_tables
- sp_cdc_cleanup_change_tables
ms.assetid: 02295794-397d-4445-a3e3-971b25e7068d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d8f81a229286a1226403d6d06aeca56fa13e8c60
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sysspcdccleanupchangetable-transact-sql"></a>sys.sp_cdc_cleanup_change_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从基于指定的当前数据库中的更改表中删除行*low_water_mark*值。 此存储过程是为需要直接管理更改表清除进程的用户提供的。 但是，由于此过程会影响更改表中数据的所有使用者，因而应多加小心。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_cdc_cleanup_change_table   
  [ @capture_instance = ] 'capture_instance',   
  [ @low_water_mark = ] low_water_mark ,  
  [ @threshold = ]'delete threshold'  
```  
  
## <a name="arguments"></a>参数  
 [ @capture_instance =] '*capture_instance*  
 与更改表关联的捕获实例的名称。 *capture_instance*是**sysname**，无默认值，并不能为 NULL。  
  
 *capture_instance*必须指定当前数据库中存在的捕获实例的名称。  
  
 [ @low_water_mark =] *low_water_mark*  
 是要使用作为新低水印的日志序列号 (LSN)*捕获实例*。 *low_water_mark*是**binary （10)**，无默认值。  
  
 如果值为非 null，则必须显示为中的当前项的 start_lsn 值[cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)表。 如果 cdc.lsn_time_mapping 中的其他条目共享与新的低水印所标识的条目相同的提交时间，则选择与该组条目关联的最小 LSN 作为低水印。  
  
 如果值显式设置为 NULL，当前*低水位线*为*捕获实例*用于定义上限的清理操作。  
  
 [ @threshold=] '*删除阈值*  
 清除时可以使用一条语句删除的删除项的最大数量。 *delete_threshold*是**bigint**，默认值为 5000。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>注释  
 sys.sp_cdc_cleanup_change_table 执行以下操作：  
  
1.  如果@low_water_mark参数不为 NULL，它将为 start_lsn 值设置*捕获实例*对新*低水位线*。  
  
    > [!NOTE]  
    >  新的低水印可能不是在存储过程调用中指定的低水印。 如果 cdc.lsn_time_mapping 表中的其他条目共享相同的提交时间，则在这组条目中表示的最小 start_lsn 将被选为调整后的低水印。 如果@low_water_mark参数为 NULL 或当前低水印大于新 lowwatermark、 的 start_lsn 值捕获实例是忽略未更改。  
  
2.  然后删除其 __$start_lsn 值小于低水印的更改表条目。 删除阈值用于限制在单个事务中删除的行数。 如果未成功删除条目，将进行报告，但不影响可能已基于此调用而对捕获实例低水印进行的任何更改。  
  
 在以下环境中使用 sys.sp_cdc_cleanup_change_table：  
  
-   清理代理作业报告删除失败。  
  
     管理员可以运行此存储过程以显式重试失败的操作。 若要重试清理给定的捕获实例，执行 sys.sp_cdc_cleanup_change_table，并指定为 NULL@low_water_mark参数。  
  
-   由清理代理作业使用的基于保留期的简单策略不能满足要求。  
  
     因为此存储过程对单个捕获实例执行清理，因此可以用它生成自定义清理策略，以便根据各个具体的捕获实例调整清理规则。  
  
## <a name="permissions"></a>Permissions  
 要求具有 db_owner 固定数据库角色中的成员资格。  
  
## <a name="see-also"></a>另请参阅  
 [cdc.fn_cdc_get_all_changes_&#60; capture_instance &#62; &#40;Transact SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_get_min_lsn &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [sys.fn_cdc_increment_lsn &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md)  
  
  
