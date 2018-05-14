---
title: EnumString 数据类型 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bb1a181a73a6e6a2f4998fb12381c522afb4e510
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="enumstring-data-type-xmla"></a>EnumString 数据类型 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  定义一个派生数据类型，该类型表示一组给定枚举器的命名常量。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<EnumString>...</EnumString>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|**字符串**|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|無|  
|派生元素|無|  
  
## <a name="remarks"></a>注释  
 XML for Analysis (XMLA) 可以使用枚举将字符串值限制为一组可验证设置。 **EnumString**使用标准的 XML**字符串**数据类型。 每个命名常量的特定值都通过枚举器定义指定。 通过将它们添加到定义枚举器[DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)架构行集，并可以通过使用检索[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法 DISCOVER_ENUMERATORS 替换请求类型。  
  
 下表描述了支持的实例的枚举数[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
|枚举器|Description|  
|----------------|-----------------|  
|ProviderType|支持的提供程序类型列中[DISCOVER_DATASOURCES](../../../analysis-services/schema-rowsets/xml/discover-datasources-rowset.md)架构行集，确定可通过返回的数据的类型[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。<br /><br /> 此枚举还支持 XMLA 属性中，**提供程序类型**，它确定支持的提供程序类型[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。 此枚举还在 DISCOVER_DATASOURCES 架构行集中使用。<br /><br /> 有关详细信息**提供程序类型**，请参阅[支持 XMLA 属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)。|  
|AuthenticationMode|支持 DISCOVER_DATASOURCES 架构行集中的 AuthenticationMode 列，该列确定为了访问 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例而必须传递的安全凭据。|  
|PropertyAccessType|支持中的 PropertyAccessType 列[DISCOVER_PROPERTIES](../../../analysis-services/schema-rowsets/xml/discover-properties-rowset.md)架构行集，确定可用于 XMLA 属性的访问的类型。|  
|StateSupport|支持 XMLA 属性**StateSupport**，它确定 statefulness 支持的级别[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。<br /><br /> 有关详细信息**StateSupport**，请参阅[支持 XMLA 属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)。|  
|StateActionVerb|包含 SOAP 标头中的 XMLA 支持的谓词列表，这些谓词用于开始、标识和结束会话。<br /><br /> 有关会话的详细信息，请参阅[管理连接和会话&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)。|  
|ResultsetFormat|支持 XMLA 属性**格式**，用于确定在返回的数据类型[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)元素。<br /><br /> 有关详细信息**格式**，请参阅[支持 XMLA 属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)。|  
|ResultsetAxisFormat|支持 XMLA 属性**AxisFormat**，它确定轴信息中返回的格式**根**包含多维数据的元素。<br /><br /> 有关详细信息**AxisFormat**，请参阅[支持 XMLA 属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)。|  
|ResultsetContents|支持 XMLA 属性**内容**，它确定是否在返回元数据**根**元素。<br /><br /> 有关详细信息**内容**，请参阅[支持 XMLA 属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)。|  
|MDXSupportLevel|支持 XMLA 属性**MDXSupport**，指示的级别上可用的多维表达式 (MDX) 支持[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。<br /><br /> 有关详细信息**MDXSupport**，请参阅[支持 XMLA 属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [XML 数据类型&#40;XMLA&#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  
