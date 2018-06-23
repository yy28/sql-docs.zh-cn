---
title: Alter 元素 (XMLA) |Microsoft 文档
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
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 5ea2c3ed3105c66b0c0848138acb5941978dd9bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026627"
---
# <a name="alter-element-xmla"></a>Alter 元素 (XMLA)
  包含所使用的 Analysis Services 脚本语言 (ASSL) 元素[执行](../xml-elements-methods-execute.md)方法，以便更改对象的实例上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
|ObjectExpansion|（可选的 `Enum` 属性）定义 `Execute` 方法所执行的更改的程度。<br /><br /> 如果设置为*ObjectProperties*、`ObjectDefinition`元素应包含仅要更改的主要对象的完整定义包括从属次要对象。 要更改的对象的从属主要对象保持不变。 **注意：** 时使用*ObjectProperties*设置，并[ClrAssembly](../../scripting/data-type/assembly-data-type-assl.md)数据类型，[数据](../../scripting/objects/data-element-assl.md)元素关联的[ClrAssemblyFile](../../scripting/data-type/clrassemblyfile-data-type-assl.md)数据类型不需要指定。 如果未指定，则 `ClrAssembly` 使用现有文件。 <br /><br /> 如果设置为*ExpandFull*、`ObjectDefinition`元素应包含不只是要更改的对象的定义，但还派生的对象，要更改的所有主要对象的定义。 **注意：** *ExpandFull*设置不能与使用[服务器](../../scripting/objects/server-element-assl.md)元素。|  
|范围|（可选的 `Enum` 属性）定义 `ObjectDefinition` 元素中定义的对象的持续时间。<br /><br /> 如果设置为*会话*中, 定义的对象`ObjectDefinition`元素只存在于 XMLA 会话的持续时间。 **注意：** 时使用*会话*设置，`ObjectDefinition`元素只能包含[维度](../../scripting/objects/dimension-element-assl.md)，[多维数据集](../../scripting/objects/cube-element-assl.md)，或[MiningModel](../../scripting/objects/miningmodel-element-assl.md) ASSL 元素。 <br /><br /> 如果忽略此属性，则 `ObjectDefinition` 元素中定义的对象将在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上一直存在。|  
  
## <a name="remarks"></a>Remarks  
 每个`Alter`命令更改指定的父对象下的一个主要对象的定义[ParentObject](../xml-elements-properties/parentobject-element-xmla.md)元素。  
  
## <a name="see-also"></a>请参阅  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  