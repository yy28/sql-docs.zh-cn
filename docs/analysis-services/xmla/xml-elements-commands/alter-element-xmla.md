---
title: Alter 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 272d202ff9bb1809e1b70261f34529523a3d8d53
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="alter-element-xmla"></a>Alter 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含所使用的 Analysis Services 脚本语言 (ASSL) 元素[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法，以便更改对象的实例上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)， [ObjectDefinition](../../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|AllowCreate|(可选**布尔**属性) 指示对象是否在中定义**Alter**应创建命令，如果不存在。<br /><br /> 如果设置为 true，在中定义的对象**ObjectDefinition**元素上创建[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例如果不存在。 换而言之， **Alter**命令将被视为**创建**命令如果对象不存在的实例上。<br /><br /> 如果省略此属性或将其设置为**false**，如果对象已不存在，则会发生错误。|  
|ObjectExpansion|(可选**枚举**属性) 定义的内容有变更由执行程度**执行**方法。<br /><br /> 如果设置为*ObjectProperties*、 **ObjectDefinition**元素应包含仅要更改的主要对象的完整定义包括从属次要对象。 要更改的对象的从属主要对象保持不变。<br /><br /> 注意： 当使用*ObjectProperties*设置，并[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)数据类型，[数据](../../../analysis-services/scripting/objects/data-element-assl.md)元素关联的[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)数据类型不需要指定。 如果未指定， **ClrAssembly**使用现有文件。<br /><br /> 如果设置为*ExpandFull*、 **ObjectDefinition**元素应包含不只是要更改的对象的定义，但还的对象派生的所有主要对象的定义要更改。<br /><br /> 注意： *ExpandFull*设置不能与使用[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)元素。|  
|范围|(可选**枚举**属性) 定义中定义的对象的持续时间**ObjectDefinition**元素。<br /><br /> 如果设置为*会话*中, 定义的对象**ObjectDefinition**元素只存在于 XMLA 会话的持续时间。<br /><br /> 注意： 当使用*会话*设置， **ObjectDefinition**元素只能包含[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)，[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)，或[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) ASSL 元素。<br /><br /> 如果省略此属性，在定义对象**ObjectDefinition**元素会保留在[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。|  
  
## <a name="remarks"></a>注释  
 每个**Alter**命令更改指定的父对象下的一个主要对象的定义[ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)元素。  
  
## <a name="see-also"></a>另请参阅  
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
