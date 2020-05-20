---
title: cdc. captured_columns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.captured_columns
- cdc.captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.captured_columns
ms.assetid: 7bb4d408-d764-4ef6-802c-f271c8d39c2a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1a635ab2284a413fb3a4cf9e11b9f40e0369f958
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832433"
---
# <a name="cdccaptured_columns-transact-sql"></a>cdc.captured_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为在捕获实例中跟踪的每一列返回一行。 默认情况下，将捕获源表中的所有列。 但是，如果为变更数据捕获启用了源表，则可以通过指定列列表将列包括在捕获范围内或排除在捕获范围之外。 有关详细信息，请参阅[sys.databases&#41;sp_cdc_enable_table &#40;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)。  
  
 建议不要**直接查询系统表**。 请改为执行[sys.databases. sp_cdc_get_source_columns](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)存储过程。  
   
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|捕获的列所属的源表 ID。|  
|column_name |**sysname**|捕获的列的名称。|  
|**column_id**|**int**|捕获的列在源表内的 ID。|  
|**column_type**|**sysname**|捕获的列的类型。|  
|**column_ordinal**|**int**|更改表中的列序号（从 1 开始）。 将排除更改表中的元数据列。 序号 1 将分配给捕获到的第一个列。|  
|**is_computed**|**bit**|表示捕获到的列是源表中计算所得的列。|  
  
## <a name="see-also"></a>另请参阅  
 [change_tables &#40;Transact-sql&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
