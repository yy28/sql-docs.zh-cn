---
title: MDSCHEMA_DIMENSIONS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e1e509ad466a0d173fe67a8fd1f3ac5190647eb7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="mdschemadimensions-rowset"></a>MDSCHEMA_DIMENSIONS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  介绍数据库中的共享维度和专用维度。  
  
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
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用以下有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**DIMENSION_VISIBILITY**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用以下有效的值之一：<br /><br /> 1 可见<br /><br /> 2 不可见|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
