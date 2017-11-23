---
title: "sys.pdw_table_distribution_properties (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 639a7475-7c92-41e0-a8ab-ad630eb5aea3
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4b0c8b3b637fbf46edb599e6ab39804ec16bac8b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwtabledistributionproperties-transact-sql"></a>sys.pdw_table_distribution_properties (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含表的分发信息。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|属性指定了哪些三个表的 ID。||  
|**distribution_policy**|**tinyint**|0 = 未定义<br /><br /> 1 = NONE<br /><br /> 2 = 哈希<br /><br /> 3 = 复制<br /><br /> 4 = ROUND_ROBIN 均可|复制仅适用于[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。|  
|**distribution_policy_desc**|**nvarchar(60)**|未定义，无、 哈希，复制，SEGMENTED_HEAP|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]返回哈希或复制。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
