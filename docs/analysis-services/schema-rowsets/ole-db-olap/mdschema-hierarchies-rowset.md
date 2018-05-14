---
title: MDSCHEMA_HIERARCHIES 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7b2be443b6059a3def3197448ef75bf89586e156
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="mdschemahierarchies-rowset"></a>MDSCHEMA_HIERARCHIES 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  介绍特定维度中的每个层次结构。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_HIERARCHIES**行集包含以下各列。  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|此层次结构所属的目录的名称。 **NULL**如果提供程序不支持目录。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|不支持|  
|**CUBE_NAME**|**DBTYPE_WSTR**|（必需）此层次结构所属的多维数据集的名称。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|此层次结构所属的维度的唯一名称。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**HIERARCHY_NAME**|**DBTYPE_WSTR**|层次结构的名称。 如果维度中仅有一个层次结构，则为空。 这将始终有一个值， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|层次结构的唯一名称。|  
|**HIERARCHY_GUID**|**DBTYPE_GUID**|不支持|  
|**HIERARCHY_CAPTION**|**DBTYPE_WSTR**|标签或标题关联的层次结构。 主要用于显示目的。 如果标题不存在， **HIERARCHY_NAME**返回。 如果维度不包含层次结构，或只有一个层次结构，则此列将包含相应维度的名称。|  
|**DIMENSION_TYPE**|**DBTYPE_I2**|维度的类型。 有效值包括下列各值：<br /><br /> **MD_DIMTYPE_UNKNOWN** (**0**)<br /><br /> **MD_DIMTYPE_TIME** (**1**)<br /><br /> **MD_DIMTYPE_MEASURE** (**2**)<br /><br /> **MD_DIMTYPE_OTHER** (**3**)<br /><br /> **MD_DIMTYPE_QUANTITATIVE** (**5**)<br /><br /> **MD_DIMTYPE_ACCOUNTS** (**6**)<br /><br /> **MD_DIMTYPE_CUSTOMERS** (**7**)<br /><br /> **MD_DIMTYPE_PRODUCTS** (**8**)<br /><br /> **MD_DIMTYPE_SCENARIO** (**9**)<br /><br /> **MD_DIMTYPE_UTILIY** (**10**)<br /><br /> **MD_DIMTYPE_CURRENCY** (**11**)<br /><br /> **MD_DIMTYPE_RATES** (**12**)<br /><br /> **MD_DIMTYPE_CHANNEL** (**13**)<br /><br /> **MD_DIMTYPE_PROMOTION** (**14**)<br /><br /> **MD_DIMTYPE_ORGANIZATION** (**15**)<br /><br /> **MD_DIMTYPE_BILL_OF_MATERIALS** (**16**)<br /><br /> **MD_DIMTYPE_GEOGRAPHY** (**17**)|  
|**HIERARCHY_CARDINALITY**|**DBTYPE_UI4**|层次结构中的成员数。|  
|**DEFAULT_MEMBER**|**DBTYPE_WSTR**|此层次结构的默认成员。 这是唯一的名称。 每个层次结构必须有一个默认成员。|  
|**ALL_MEMBER**|**DBTYPE_WSTR**|汇总中最高级别的成员。|  
|**DESCRIPTION**|**DBTYPE_WSTR**|层次结构的可读说明。 **NULL**如果没有任何其他说明存在。|  
|**结构**|**DBTYPE_I2**|层次结构的结构。 有效值包括下列各值：<br /><br /> **MD_STRUCTURE_FULLYBALANCED** (**0**)<br /><br /> **MD_STRUCTURE_RAGGEDBALANCED** (**1**)<br /><br /> **MD_STRUCTURE_UNBALANCED** (**2**)<br /><br /> **MD_STRUCTURE_NETWORK** (**3**)|  
|**IS_VIRTUAL**|**DBTYPE_BOOL**|始终返回**False**。|  
|**IS_READWRITE**|**DBTYPE_BOOL**|一个布尔值，指示是否启用写回到维度列。<br /><br /> 返回**TRUE**如果**编写回到维度**启用表示此层次结构的列。|  
|**DIMENSION_UNIQUE_SETTINGS**|**DBTYPE_I4**|始终返回**MDDIMENSIONS_MEMBER_KEY_UNIQUE** (**1**)。|  
|**DIMENSION_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|始终返回**NULL**。|  
|**DIMENSION_IS_VISIBLE**|**DBTYPE_BOOL**|始终返回**true**。 如果相应维度不可见，则也不会在架构行集中显示该维度。|  
|**HIERARCHY_ORDINAL**|**DBTYPE_UI4**|多维数据集的所有层次结构的层次结构序号。|  
|**DIMENSION_IS_SHARED**|**DBTYPE_BOOL**|始终返回**TRUE**。|  
|**HIERARCHY_IS_VISIBLE**|**DBTYPE_BOOL**|指示层次结构是否可见的布尔值。<br /><br /> 返回**TRUE**如果层次结构是可见的; 否则为**FALSE**。|  
|**HIERARCHY_ORIGIN**|**DBTYPE_UI2**|确定层次结构源的位掩码：<br /><br /> **MD_USER_DEFINED**标识用户定义层次结构和的值为**0x0000001**。<br /><br /> **MD_SYSTEM_ENABLED**标识属性层次结构和的值为**0x0000002**。<br /><br /> **MD_SYSTEM_INTERNAL**标识属性具有任何属性层次结构中，和的值为**0x0000004**。<br /><br /> <br /><br /> 请注意，父/子属性层次结构是同时**MD_USER_DEFINED**和**MD_SYSTEM_ENABLED**。|  
|**HIERARCHY_DISPLAY_FOLDER**|**DBTYPE_WSTR**|在用户界面中显示层次结构时需使用的路径。 文件夹名称将由分号 (;) 分隔。 通过反斜杠来指示嵌套的文件夹 (\\)。|  
|**INSTANCE_SELECTION**|**DBTYPE_UI2**|向客户端应用程序提供的有关如何显示层次结构的提示。 有效值包括下列各值：<br /><br /> **MD_INSTANCE_SELECTION_NONE**<br /><br /> **MD_INSTANCE_SELECTION_DROPDOWN**<br /><br /> **MD_INSTANCE_SELECTION_LIST**<br /><br /> **MD_INSTANCE_SELECTION_FILTEREDLIST**<br /><br /> **MD_INSTANCE_SELECTION_MANDATORYFILTER**|  
|**GROUPING_BEHAVIOR**|**DBTYPE_I2**|指定此层次结构的客户端的预期分组行为的枚举。 可能的值如下：<br /><br /> **EncourageGrouping** (1)<br /><br /> **DiscourageGrouping** (2)|  
|**STRUCTURE_TYPE**|**DBTYPE_WSTR**|指示层次结构的类型。 有效值包括下列各值：<br /><br /> **自然**<br /><br /> **自然**<br /><br /> **Unknown**|  
  
 行集按排序**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**， **DIMENSION_UNIQUE_NAME**， **HIERARCHY_名称**。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_HIERARCHIES**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**HIERARCHY_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**HIERARCHY_ORIGIN**|**DBTYPE_UI2**|（可选）默认限制对 MD_USER_DEFINED 和 MD_SYSTEM_ENABLED 有效。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用以下有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**HIERARCHY_VISIBILITY**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用以下有效的值之一：<br /><br /> 1 可见<br /><br /> 2 不可见|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
