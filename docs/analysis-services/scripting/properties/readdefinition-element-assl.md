---
title: ReadDefinition 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c1de83a87874aa902e19b007641477399b8040c2
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="readdefinition-element-assl"></a>ReadDefinition 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  确定成员是否可以读取数据库的定义或数据库中对象的定义。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Permission> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <ReadDefinition>...</ReadDefinition>  
   ...  
</Permission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*无*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)， [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)， [DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)， [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)，[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*InclusionThresholdSetting*|不允许访问对象定义。|  
|*基本*|允许对对象定义进行基本访问。<br /><br /> 注意： 此权限是必需创建本地多维数据集、 链接度量值组和链接维度。|  
|*允许*|允许对对象定义进行完全的访问。<br /><br /> 注意： 此权限是必需执行[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)XML for Analysis (XMLA) 调用使用 DISCOVER_XML_METADATA 参数。|  
  
 对应的父级的元素**ReadDefinition**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CubePermission>， <xref:Microsoft.AnalysisServices.DatabasePermission>， <xref:Microsoft.AnalysisServices.DimensionPermission>， <xref:Microsoft.AnalysisServices.MiningModelPermission>， <xref:Microsoft.AnalysisServices.MiningStructurePermission>，和<xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>另请参阅  
 [Role 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
