---
title: LNum 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 49ab7672d51a90e30701666fbf391ffec6060f29
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575469"
---
# <a name="lnum-element-xmla"></a>LNum 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含父级的级别序号位置有关的信息[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md)或[成员](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <LNum>...</LNum>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|ssNoversion|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md)，[成员](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 有关**HierarchyInfo**元素， **LNum**元素包含提供层次结构的级别序号位置的属性的名称。 其值等效于 OLE DB for OLAP 规范中为轴行集定义的 LEVEL_NUMBER 属性。  
  
 有关**成员**元素， **LNum**元素包含的从零开始序号位置，从层次结构的根级别的成员表示，则父级[成员](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)元素。 值零表示层次结构的根级别。  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
