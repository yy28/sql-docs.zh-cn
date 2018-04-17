---
title: syscollector_collector_types (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syscollector_collector_types
- syscollector_collector_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_collector_types view
ms.assetid: d5cd30bb-89fd-4814-a7e8-9074f043f90f
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 889c23db91765fb70d713d34c1356aea2e71d9a6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="syscollectorcollectortypes-transact-sql"></a>syscollector_collector_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供有关收集项的收集器类型的信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**collector_type_uid**|**uniqueidentifer**|收集类型的 GUID。 不可为 null。|  
|**名称**|**sysname**|收集类型的名称。 不可为 null。|  
|**parameter_schema**|**xml**|描述指定收集器类型的配置情况的 XML 架构。 此 XML 架构用于验证与特定收集项实例相关联的实际 XML 配置。 可以为 Null。|  
|**parameter_formatter**|**xml**|确定用于转换 XML 的模板，以便在收集组属性页中使用。 可以为 Null。|  
|**collection_package_id**|**uniqueidentifer**|收集包的 GUID。 不可为 null。|  
|**collection_package_path**|**nvarchar(4000)**|提供收集包的路径。 可以为 Null。|  
|**collection_package_name**|**sysname**|收集包的名称。 不可为 null。|  
|**upload_package_id**|**uniqueidentifer**|上载包的 GUID。 不可为 null。|  
|**upload_package_path**|**nvarchar(4000)**|提供上载包的路径。 可以为 Null。|  
|**upload_package_name**|**sysname**|上载包的名称。 不可为 null。|  
|**is_system**|**bit**|(1) 打开或关闭的 (0)，以指示如果收集器类型随数据收集器或更高版本通过添加**dc_admin**。 这可以是内部开发的或由第三方开发的自定义类型。 不可为 null。|  
  
## <a name="permissions"></a>权限  
 需要为选择**dc_operator**， **dc_proxy**。  
  
## <a name="change-history"></a>更改历史记录  
  
|更新内容|  
|---------------------|  
|更新**collection_type_uid**到的列名称**collector_type_uid**。|  
|更正的说明**parameter_schema**指示的值是可以为 null 的列。|  
|添加**parameter_formatter**列。|  
|更正的数据类型**collection_package_path**列，并更新描述以指明的值是可以为 null。|  
|更正的数据类型**upload_package_path**列，并更新描述以指明的值是可以为 null。|  
  
## <a name="see-also"></a>另请参阅  
 [数据收集器存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [数据收集器视图 (Transact-SQL)](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [“数据收集”](../../relational-databases/data-collection/data-collection.md)  
  
  
