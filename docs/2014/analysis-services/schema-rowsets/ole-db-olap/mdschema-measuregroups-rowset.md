---
title: MDSCHEMA_MEASUREGROUPS 行集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_MEASUREGROUPS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEASUREGROUPS rowset
ms.assetid: bab1bbd0-421b-4fad-9aee-e6511e0e1f1b
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7846fa9eb88a91a945c787cfec0fe19d0c520cf6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300977"
---
# <a name="mdschemameasuregroups-rowset"></a>MDSCHEMA_MEASUREGROUPS 行集
  介绍数据库中的度量值组。  
  
## <a name="rowset-columns"></a>行集列  
 `MDSCHEMA_MEASUREGROUPS`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||此度量值组所属的目录的名称。 如果提供程序不支持目录，则为 `NULL`。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不提供支持。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||此度量值组所属的多维数据集的名称。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||度量值组的名称。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||用户可以阅读的成员说明。|  
|`IS_WRITE_ENABLED`|`DBTYPE_BOOL`||一个布尔值，指示度量值组是否已启用写操作。<br /><br /> 如果对度量值组启用了写操作，则返回 `true`。|  
|`MEASUREGROUP_CAPTION`|`DBTYPE_WSTR`||度量值组的显示标题。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 可以使用以下表中的列对 `MDSCHEMA_MEASUREGROUPS` 行集进行限制。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|可选。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|可选。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`|可选。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB for OLAP 架构行集](ole-db-for-olap-schema-rowsets.md)  
  
  
