---
title: sys.workload_management_workload_classifiers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2019
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: f3ce2327034a9c7197e754dac01dfb9e6f9dc3e5
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58509584"
---
# <a name="sysworkloadmanagementworkloadclassifiers-transact-sql-preview"></a>sys.workload_management_workload_classifiers (TRANSACT-SQL) （预览版）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 返回工作负荷分类器的详细信息。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|分类器的唯一 ID。 不可为 Null。||
group_name|**sysname**|分类器所分配到的工作负荷组的名称。 不可为 null。 |静态资源类</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80 </br> </br>动态资源类</br>smallrc</br>mediumrc</br>largerc</br>xlargerc|
NAME|**sysname**|分类器的名称。 必须是唯一的实例。 不可为 null。||
|importance|**sysname**|为此工作负荷组中以及跨共享资源的工作负荷组的请求的相对重要性。  分类器中指定的重要性重写工作负荷组的重要性设置。|低，below_normal、 普通、 above_normal 高 |
|create_time|**datetime**|分类器的创建时间。 不可为 null。||
modify_time|**datetime**|分类器的上次修改时间。 不可为 null。||
is_enabled|**bit**|显示是否已启用分类器。 默认情况下启用。 不可为 null。|0 = 未启用分类器 </br> 1 = 启用分类器|
|&nbsp;||||
  
## <a name="permissions"></a>权限

需要 VIEW SERVER STATE 权限。

## <a name="next-steps"></a>后续步骤

 适用于 SQL 数据仓库和并行数据仓库的所有目录视图的列表，请参阅[SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)。 若要创建工作负荷分类器，请参阅[创建工作负荷分类器](../../t-sql/statements/create-workload-classifier-transact-sql.md)。 工作负荷分类的详细信息，请参阅[SQL 数据仓库工作负荷分类](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
