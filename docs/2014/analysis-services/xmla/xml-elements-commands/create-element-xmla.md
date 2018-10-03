---
title: Create 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Create Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Create
- urn:schemas-microsoft-com:xml-analysis#Create
- microsoft.xml.analysis.create
helpviewer_keywords:
- Create command (XMLA)
ms.assetid: a623d362-a1ac-40e4-8816-65fac89cb391
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b64f6b222793fdd7c6b92e7462fc10976c0bc139
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051287"
---
# <a name="create-element-xmla"></a>Create 元素 (XMLA)
  包含所使用的 Analysis Services 脚本语言 (ASSL) 元素`Execute`方法来创建对象上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Create Scope="enum" AllowOverwrite="boolean">  
      <ParentObject>...</ParentObject>  
      <ObjectDefinition>...</ObjectDefinition>  
   </Create>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[ObjectDefinition](../xml-elements-properties/objectdefinition-element-xmla.md)， [ParentObject](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|AllowOverwrite|可选`Boolean`属性。 如果设置为 True，则 `ObjectDefinition` 元素中定义的对象可覆盖 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上的现有对象。 如果忽略此属性或将其设置为 False，则存在现有对象时将生成一个错误。|  
|范围|可选`Enum`属性。 定义 `ObjectDefinition` 元素中所定义对象的持续时间。 如果忽略此属性，则 `ObjectDefinition` 元素中定义的对象将在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上一直存在。 可用值如下：<br /><br /> -   *会话*<br />     `ObjectDefinition` 元素中定义的对象只在 XML for Analysis (XMLA) 会话持续期间存在。 **注意：** 使用时*会话*设置，请`ObjectDefinition`元素只能包含[维度](../../scripting/objects/dimension-element-assl.md)，[多维数据集](../../scripting/objects/cube-element-assl.md)，或[MiningModel](../../scripting/objects/miningmodel-element-assl.md) ASSL 元素。|  
  
## <a name="remarks"></a>备注  
 每个 `Create` 操作都会在 `ParentObject` 元素所指定的父级下创建一个主要对象。 如果忽略该父对象，则会将它假定为目标 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例。 如果主要对象的父级不是目标实例，则会产生错误。  
  
## <a name="example"></a>示例  
 以下示例在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上创建了一个名为 `Test Database` 的空数据库。  
  
```  
  
      <Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
   <ObjectDefinition>  
      <Database xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
         <Name>Test Database</Name>  
         <Description>A test database.</Description>  
      </Database>  
   </ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>请参阅  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
