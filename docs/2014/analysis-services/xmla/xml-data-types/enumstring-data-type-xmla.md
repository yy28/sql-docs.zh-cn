---
title: EnumString 数据类型 (XMLA) |Microsoft Docs
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
- EnumString Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EnumString
- urn:schemas-microsoft-com:xml-analysis#EnumString
- http://schemas.microsoft.com/analysisservices/2003/engine#EnumString
helpviewer_keywords:
- EnumString data type
ms.assetid: 9214195e-4539-419b-95ec-b7aa75e033ab
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ea4f9057c05d7be5a5f8d8591d27460540a377fe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37224011"
---
# <a name="enumstring-data-type-xmla"></a>EnumString 数据类型 (XMLA)
  定义一个派生数据类型，该类型表示一组给定枚举器的命名常量。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<EnumString>...</EnumString>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|`string`|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|InclusionThresholdSetting|  
|派生元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 XML for Analysis (XMLA) 可以使用枚举将字符串值限制为一组可验证设置。 `EnumString` 可以使用标准 XML `string` 数据类型。 每个命名常量的特定值都通过枚举器定义指定。 通过将它们添加到定义枚举器[DISCOVER_ENUMERATORS](../../schema-rowsets/xml/discover-enumerators-rowset.md)架构行集，并可以通过使用检索[Discover](../xml-elements-methods-discover.md)方法替换 DISCOVER_ENUMERATORS 请求类型。  
  
 下表描述了支持的实例的枚举器[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
|枚举器|Description|  
|----------------|-----------------|  
|ProviderType|支持集中的 ProviderType 列[DISCOVER_DATASOURCES](../../schema-rowsets/xml/discover-datasources-rowset.md)确定可以返回的数据类型的架构行集[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。<br /><br /> 此枚举还支持 XMLA 属性 `ProviderType`，该属性确定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例支持的访问接口类型。 此枚举还在 DISCOVER_DATASOURCES 架构行集中使用。<br /><br /> 有关详细信息`ProviderType`，请参阅[支持的 XMLA 属性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。|  
|AuthenticationMode|支持 DISCOVER_DATASOURCES 架构行集中的 AuthenticationMode 列，该列确定为了访问 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例而必须传递的安全凭据。|  
|PropertyAccessType|支持集中的 Propertyaccess 列[DISCOVER_PROPERTIES](../../schema-rowsets/xml/discover-properties-rowset.md)确定 XMLA 属性可用的访问类型的架构行集。|  
|StateSupport|支持 XMLA 属性 `StateSupport`，该属性确定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例支持的有状态级别。<br /><br /> 有关详细信息`StateSupport`，请参阅[支持的 XMLA 属性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。|  
|StateActionVerb|包含 SOAP 标头中的 XMLA 支持的谓词列表，这些谓词用于开始、标识和结束会话。<br /><br /> 有关会话的详细信息，请参阅[管理连接和会话&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)。|  
|ResultsetFormat|支持 XMLA 属性`Format`，用于确定在返回的数据类型[根](../xml-elements-properties/root-element-xmla.md)元素。<br /><br /> 有关详细信息`Format`，请参阅[支持的 XMLA 属性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。|  
|ResultsetAxisFormat|支持 XMLA 属性 `AxisFormat`，该属性确定 `root` 元素中返回的轴信息（包含多维数据）的格式。<br /><br /> 有关详细信息`AxisFormat`，请参阅[支持的 XMLA 属性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。|  
|ResultsetContents|支持 XMLA 属性 `Content`，该属性确定 `root` 元素中返回的是元数据还是数据。<br /><br /> 有关详细信息`Content`，请参阅[支持的 XMLA 属性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。|  
|MDXSupportLevel|支持 XMLA 属性 `MDXSupport`，该属性指示 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例可用的多维表达式 (MDX) 支持的级别。<br /><br /> 有关详细信息`MDXSupport`，请参阅[支持的 XMLA 属性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。|  
  
## <a name="see-also"></a>请参阅  
 [XML 数据类型&#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  
