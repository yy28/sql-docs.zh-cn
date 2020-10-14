---
description: 'sys.pdw_column_distribution_properties (Transact-sql) '
title: 'sys.pdw_column_distribution_properties (Transact-sql) '
ms.custom: seo-dt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 46b74f99-2e22-4dbd-872a-533fce0e239c
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 83bdcf74beb32e7fd5425ca56dcdd79c7c0d3d6c
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035769"
---
# <a name="syspdw_column_distribution_properties-transact-sql"></a>sys.pdw_column_distribution_properties (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存列的分发信息。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|列所属对象的 ID。||  
|column_id|**int**|列的 ID。||  
|**distribution_ordinal**|**tinyint**|分布中基于 (1 的) 顺序。|0 = 不是分布列。 1 = [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 使用此列来分布父表。|  
  
## <a name="see-also"></a>另请参阅  
 [Azure Synapse Analytics 和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
