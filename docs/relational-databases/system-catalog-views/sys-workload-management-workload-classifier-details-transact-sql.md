---
title: sys.workload_management_workload_classifier_details (TRANSACT-SQL) |Microsoft Docs
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
ms.openlocfilehash: 421f47aee86c2e5bbdffe485ffea0cffef73bafd
ms.sourcegitcommit: 05bb10710489bef16bb2c53b3803e9b8eea1429a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "57988773"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql-preview"></a>sys.workload_management_workload_classifier_details (TRANSACT-SQL) （预览版）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  返回每个分类器的详细信息。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|分类器的 ID。 向可加入[sys.workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md)。 不可为 null。|
|classifier_type|**sysname**|对其分类实体。 不可为 null。|[SQL 数据仓库工作负荷分类](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)|
|classifier_value|**sysname**|分类器的值。 不可为 null。||

## <a name="permissions"></a>权限

需要 VIEW SERVER STATE 权限。

## <a name="next-steps"></a>后续步骤
  
 适用于 SQL 数据仓库和并行数据仓库的所有目录视图的列表，请参阅[SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)。 若要创建工作负荷分类器，请参阅[创建工作负荷分类器](../../t-sql/statements/create-workload-classifier-transact-sql.md)。 工作负荷分类的详细信息，请参阅[SQL 数据仓库工作负荷分类](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
