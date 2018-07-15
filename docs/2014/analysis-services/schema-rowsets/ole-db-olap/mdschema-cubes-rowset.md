---
title: MDSCHEMA_CUBES 行集 |Microsoft Docs
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
- MDSCHEMA_CUBES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_CUBES rowset
ms.assetid: 5f1b63d4-aa3f-48c6-b866-7ffd91675044
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 441f83b4b5bec1a2340fbf6e8a3b14da77363162
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243397"
---
# <a name="mdschemacubes-rowset"></a>MDSCHEMA_CUBES 行集
  介绍数据库中的多维数据集的结构。  
  
## <a name="rowset-columns"></a>行集列  
 `MDSCHEMA_CUBES`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||数据库的名称。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不提供支持。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||多维数据集或维度的名称。 维度名称以美元符号 ($) 开头。 **注意：** 只有服务器管理员和数据库管理员有权查看通过维度创建多维数据集。|  
|`CUBE_TYPE`|`DBTYPE_WSTR`||多维数据集的类型。 有效值为<br /><br /> -   `CUBE`<br />-   `DIMENSION`|  
|`CUBE_GUID`|`DBTYPE_GUID`||不提供支持。|  
|`CREATED_ON`|`DBTYPE_DBTIMESTAMP`||不提供支持。|  
|`LAST_SCHEMA_UPDATE`|`DBTYPE_DBTIMESTAMP`||上次处理相应多维数据集的时间。|  
|`SCHEMA_UPDATED_BY`|`DBTYPE_WSTR`||不提供支持。|  
|`LAST_DATA_UPDATE`|`DBTYPE_DBTIMESTAMP`||上次处理相应多维数据集的时间。|  
|`DATA_UPDATED_BY`|`DBTYPE_WSTR`||不提供支持。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||多维数据集的用户友好说明。|  
|`IS_DRILLTHROUGH_ENABLED`|`DBTYPE_BOOL`||一个布尔值，它始终返回 true。|  
|`IS_LINKABLE`|`DBTYPE_BOOL`||一个布尔值，指示是否可以在链接多维数据集中使用多维数据集。|  
|`IS_WRITE_ENABLED`|`DBTYPE_BOOL`||一个布尔值，指示多维数据集是否已启用写操作。|  
|`IS_SQL_ENABLED`|`DBTYPE_BOOL`||一个布尔值，指示是否可以对多维数据集使用 SQL。|  
|`CUBE_CAPTION`|`DBTYPE_WSTR`||多维数据集的标题。|  
|`BASE_CUBE_NAME`|`DBTYPE_WSTR`||如果相应多维数据集为透视多维数据集，则为源多维数据集的名称。|  
|`ANNOTATIONS`|`DBTYPE_WSTR`||（可选）一组格式为 XML 的注释。|  
  
 行集按 `CATALOG_NAME`、`SCHEMA_NAME`、`CUBE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制列  
 `MDSCHEMA_CUBES`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|可选。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|（可选）具有以下任一有效值的位图：<br /><br /> -1 的多维数据集<br />-2 个维度<br /><br /> 默认限制的值为 1。|  
|`Base Cube_Name`|`DBTYPE_WSTR`|可选。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB for OLAP 架构行集](ole-db-for-olap-schema-rowsets.md)  
  
  
