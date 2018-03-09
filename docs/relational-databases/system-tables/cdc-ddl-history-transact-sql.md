---
title: "cdc.ddl_history (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- cdc.ddl_history_TSQL
- cdc.ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.ddl_history
ms.assetid: cb97ea71-da2f-441a-bbd2-db1f5f48ab49
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26ce592636c837f74cbbc8980b5d7cbd8742f78a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="cdcddlhistory-transact-sql"></a>cdc.ddl_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为对启用了变更数据捕获的表所做的每一项数据定义语言 (DDL) 更改返回一行。 可以使用此表来确定源表发生 DDL 更改的时间以及更改的内容。 此表中不包含未发生 DDL 更改的源表的任何条目。  
  
 我们建议您不要直接查询系统表， 相反，执行[sys.sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)存储过程。  
   
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**source_object_id**|**int**|应用 DDL 更改的源表的 ID。|  
|**object_id**|**int**|与源表的捕获实例相关联的更改表的 ID。|  
|**required_column_update**|**bit**|指示在源表中修改了捕获列的数据类型。 此修改改变了更改表中的列。|  
|**ddl_command**|**nvarchar(max)**|应用于源表的 DDL 语句。|  
|**ddl_lsn**|**binary(10)**|与 DDL 修改的提交相关联的日志序列号 (LSN)。|  
|**ddl_time**|**datetime**|对源表所做的 DDL 更改的日期和时间。|  
  
## <a name="see-also"></a>另请参阅  
 [sys.sp_cdc_help_change_data_capture &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60; capture_instance &#62; &#40;Transact SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
