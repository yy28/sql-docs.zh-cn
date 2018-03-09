---
title: "MDSCHEMA_DIMENSIONS 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDSCHEMA_DIMENSIONS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_DIMENSIONS rowset
ms.assetid: a0fd94bb-359a-4df6-93a6-d60d50223944
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5cf0198759485452fc3fd6d82cdd2642df92b440
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="mdschemadimensions-rowset"></a>MDSCHEMA_DIMENSIONS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]描述在数据库中的共享和私有维度。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_DIMENSIONS**行集包含以下列：  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|数据库的名称。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|不提供支持。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|多维数据集的名称。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|维度的名称。 如果相应维度不止是一个多维数据集或度量值组的一部分，则针对每个唯一的维度/度量值组和维度/多维数据集组合都有一行。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|维度的唯一名称。|  
|**DIMENSION_GUID**|**DBTYPE_GUID**|不提供支持。|  
|**DIMENSION_CAPTION**|**DBTYPE_WSTR**|维度的标题。 应在向用户显示维度的名称（例如在用户界面或报告中）时使用维度标题。|  
|**DIMENSION_ORDINAL**|**DBTYPE_UI4**|维度在多维数据集中的位置。|  
|**DIMENSION_TYPE**|**DBTYPE_I2**|维度的类型。 有效值包括：<br /><br /> **MD_DIMTYPE_UNKNOWN** (**0**)<br /><br /> **MD_DIMTYPE_TIME** (**1**)<br /><br /> **MD_DIMTYPE_MEASURE** (**2**)<br /><br /> **MD_DIMTYPE_OTHER** (**3**)<br /><br /> **MD_DIMTYPE_QUANTITATIVE** (**5**)<br /><br /> **MD_DIMTYPE_ACCOUNTS** (**6**)<br /><br /> **MD_DIMTYPE_CUSTOMERS** (**7**)<br /><br /> **MD_DIMTYPE_PRODUCTS** (**8**)<br /><br /> **MD_DIMTYPE_SCENARIO** (**9**)<br /><br /> **MD_DIMTYPE_UTILIY** (**10**)<br /><br /> **MD_DIMTYPE_CURRENCY** (**11**)<br /><br /> **MD_DIMTYPE_RATES** (**12**)<br /><br /> **MD_DIMTYPE_CHANNEL** (**13**)<br /><br /> **MD_DIMTYPE_PROMOTION** (**14**)<br /><br /> **MD_DIMTYPE_ORGANIZATION** (**15**)<br /><br /> **MD_DIMTYPE_BILL_OF_MATERIALS** (**16**)<br /><br /> **MD_DIMTYPE_GEOGRAPHY** (**17**)|  
|**DIMENSION_CARDINALITY**|**DBTYPE_UI4**|键属性中的成员数。|  
|**DEFAULT_HIERARCHY**|**DBTYPE_WSTR**|维度的层次结构。 保留层次结构是为了向后兼容。|  
|**DESCRIPTION**|**DBTYPE_WSTR**|维度的用户友好说明。|  
|**IS_VIRTUAL**|**DBTYPE_BOOL**|始终**FALSE**。|  
|**IS_READWRITE**|**DBTYPE_BOOL**|一个布尔值，指示维度是否已启用写操作。<br /><br /> **TRUE**如果维度是启用写功能。|  
|**DIMENSION_UNIQUE_SETTINGS**|**DBTYPE_I4**|如果维度只包含具有唯一名称的成员，则为指定包含唯一值的列的位图。 下列位值常量是在此位图的 Msmd.h 中定义的：<br /><br /> **MDDIMENSIONS_MEMBER_KEY_UNIQUE**|  
|**DIMENSION_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|始终**NULL**。|  
|**DIMENSION_IS_VISIBLE**|**DBTYPE_BOOL**|始终**TRUE**。<br /><br /> 注意： 除非维度中的一个或多个层次结构可见，否则，维度不可见。|  
  
 行集按排序**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**， **DIMENSION_NAME**。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_DIMENSIONS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|可选。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|可选。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|可选。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用以下有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**DIMENSION_VISIBILITY**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用以下有效的值之一：<br /><br /> 1 可见<br /><br /> 2 不可见|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
