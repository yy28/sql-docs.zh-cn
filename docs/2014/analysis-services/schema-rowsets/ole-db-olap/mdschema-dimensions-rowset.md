---
title: MDSCHEMA_DIMENSIONS 行集 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_DIMENSIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_DIMENSIONS rowset
ms.assetid: a0fd94bb-359a-4df6-93a6-d60d50223944
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b00b617adf90e1dba8eac94a9872ce07c0773e7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016484"
---
# <a name="mdschemadimensions-rowset"></a>MDSCHEMA_DIMENSIONS 行集
  介绍数据库中的共享维度和专用维度。  
  
## <a name="rowset-columns"></a>行集列  
 `MDSCHEMA_DIMENSIONS` 行集包含以下列：  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||数据库的名称。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不提供支持。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||多维数据集的名称。|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||维度的名称。 如果相应维度不止是一个多维数据集或度量值组的一部分，则针对每个唯一的维度/度量值组和维度/多维数据集组合都有一行。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||维度的唯一名称。|  
|`DIMENSION_GUID`|`DBTYPE_GUID`||不提供支持。|  
|`DIMENSION_CAPTION`|`DBTYPE_WSTR`||维度的标题。 应在向用户显示维度的名称（例如在用户界面或报告中）时使用维度标题。|  
|`DIMENSION_ORDINAL`|`DBTYPE_UI4`||维度在多维数据集中的位置。|  
|`DIMENSION_TYPE`|`DBTYPE_I2`||维度的类型。 有效值包括：<br /><br /> -   `MD_DIMTYPE_UNKNOWN` (`0`)<br />-   `MD_DIMTYPE_TIME` (`1`)<br />-   `MD_DIMTYPE_MEASURE` (`2`)<br />-   `MD_DIMTYPE_OTHER` (`3`)<br />-   `MD_DIMTYPE_QUANTITATIVE` (`5`)<br />-   `MD_DIMTYPE_ACCOUNTS` (`6`)<br />-   `MD_DIMTYPE_CUSTOMERS` (`7`)<br />-   `MD_DIMTYPE_PRODUCTS` (`8`)<br />-   `MD_DIMTYPE_SCENARIO` (`9`)<br />-   `MD_DIMTYPE_UTILIY` (`10`)<br />-   `MD_DIMTYPE_CURRENCY` (`11`)<br />-   `MD_DIMTYPE_RATES` (`12`)<br />-   `MD_DIMTYPE_CHANNEL` (`13`)<br />-   `MD_DIMTYPE_PROMOTION` (`14`)<br />-   `MD_DIMTYPE_ORGANIZATION` (`15`)<br />-   `MD_DIMTYPE_BILL_OF_MATERIALS` (`16`)<br />-   `MD_DIMTYPE_GEOGRAPHY` (`17`)|  
|`DIMENSION_CARDINALITY`|`DBTYPE_UI4`||键属性中的成员数。|  
|`DEFAULT_HIERARCHY`|`DBTYPE_WSTR`||维度的层次结构。 保留层次结构是为了向后兼容。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||维度的用户友好说明。|  
|`IS_VIRTUAL`|`DBTYPE_BOOL`||始终为 `FALSE`。|  
|`IS_READWRITE`|`DBTYPE_BOOL`||一个布尔值，指示维度是否已启用写操作。<br /><br /> 如果已对维度启用了写操作，则为 `TRUE`。|  
|`DIMENSION_UNIQUE_SETTINGS`|`DBTYPE_I4`||如果维度只包含具有唯一名称的成员，则为指定包含唯一值的列的位图。 下列位值常量是在此位图的 Msmd.h 中定义的：<br /><br /> -   `MDDIMENSIONS_MEMBER_KEY_UNIQUE`|  
|`DIMENSION_MASTER_UNIQUE_NAME`|`DBTYPE_WSTR`||始终为 `NULL`。|  
|`DIMENSION_IS_VISIBLE`|`DBTYPE_BOOL`||始终为 `TRUE`。 **注意：** 维度不可见，除非是可见的维度中的一个或多个层次结构。|  
  
 行集按 `CATALOG_NAME`、`SCHEMA_NAME`、`CUBE_NAME`、`DIMENSION_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制列  
 `MDSCHEMA_DIMENSIONS`行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|可选。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|可选。|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`|可选。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|（可选）位图，并使用以下有效的值之一：<br /><br /> -1 的多维数据集<br />-2 的维度<br /><br /> 默认限制的值为 1。|  
|`DIMENSION_VISIBILITY`|`DBTYPE_UI2`|（可选）位图，并使用以下有效的值之一：<br /><br /> -1 的可见性<br />-2 不可见<br /><br /> 默认限制的值为 1。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB for OLAP 架构行集](ole-db-for-olap-schema-rowsets.md)  
  
  