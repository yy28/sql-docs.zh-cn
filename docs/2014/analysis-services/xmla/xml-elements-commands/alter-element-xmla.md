---
title: Alter 元素 (XMLA) |Microsoft Docs
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
- Alter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Alter
- microsoft.xml.analysis.alter
- urn:schemas-microsoft-com:xml-analysis#Alter
helpviewer_keywords:
- Alter command
ms.assetid: 84e58385-c9ba-48fa-a867-94d35b777a56
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e13819d301af842eb2094d7b6ad3367cde424c72
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192404"
---
# <a name="alter-element-xmla"></a>Alter 元素 (XMLA)
  包含所使用的 Analysis Services 脚本语言 (ASSL) 元素[Execute](../xml-elements-methods-execute.md)方法，以便更改对象的实例上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Alter Scope="enum" AllowCreate="boolean" ObjectExpansion="enum">  
      <Object>...</Object>  
      <ObjectDefinition>...</ObjectDefinition>  
   </Alter>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[对象](../xml-elements-properties/object-element-xmla.md)， [ObjectDefinition](../xml-elements-properties/objectdefinition-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|AllowCreate|（可选的 `Boolean` 属性）指示当 `Alter` 命令中定义的对象不存在时，是否应创建相应对象。<br /><br /> 如果设置为 True，则当 `ObjectDefinition` 元素中定义的对象不存在时，将在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上创建相应对象。 也就是说，当实例上不存在这些对象时，`Alter` 命令可视为 `Create` 命令。<br /><br /> 如果将此属性忽略或设置为 `false`，则相应对象不存在时将引发一个错误。|  
|ObjectExpansion|（可选的 `Enum` 属性）定义 `Execute` 方法所执行的更改的程度。<br /><br /> 如果设置为*ObjectProperties*，则`ObjectDefinition`元素应包含仅要更改该主要对象的完整定义包括从属次级对象。 要更改的对象的从属主要对象保持不变。 **注意：** 使用时*ObjectProperties*设置为设置[ClrAssembly](../../scripting/data-type/assembly-data-type-assl.md)数据类型[数据](../../scripting/objects/data-element-assl.md)元素关联的[ClrAssemblyFile](../../scripting/data-type/clrassemblyfile-data-type-assl.md)不需要指定数据类型。 如果未指定，则 `ClrAssembly` 使用现有文件。 <br /><br /> 如果设置为*ExpandFull*，则`ObjectDefinition`元素应包含不只是要更改的对象的定义，但还后代对象的要更改所有主要对象的定义。 **注意：** *ExpandFull*设置不能与使用[Server](../../scripting/objects/server-element-assl.md)元素。|  
|范围|（可选的 `Enum` 属性）定义 `ObjectDefinition` 元素中定义的对象的持续时间。<br /><br /> 如果设置为*会话*中, 定义的对象`ObjectDefinition`元素只存在于 XMLA 会话持续时间。 **注意：** 使用时*会话*设置，请`ObjectDefinition`元素只能包含[维度](../../scripting/objects/dimension-element-assl.md)，[多维数据集](../../scripting/objects/cube-element-assl.md)，或[MiningModel](../../scripting/objects/miningmodel-element-assl.md) ASSL 元素。 <br /><br /> 如果忽略此属性，则 `ObjectDefinition` 元素中定义的对象将在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上一直存在。|  
  
## <a name="remarks"></a>Remarks  
 每个`Alter`命令将更改指定的父对象下的一个主要对象的定义[ParentObject](../xml-elements-properties/parentobject-element-xmla.md)元素。  
  
## <a name="see-also"></a>请参阅  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
