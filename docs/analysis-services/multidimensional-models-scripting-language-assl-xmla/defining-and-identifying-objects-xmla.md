---
title: "定义和标识对象 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- objects [XML for Analysis]
- identifying objects [XML for Analysis]
- XML for Analysis, objects
- object references [XML for Analysis]
- object identifiers [XML for Analysis]
- object definitions [XML for Analysis]
- XMLA, objects
ms.assetid: 43b65f6d-0123-4556-81f0-c7a0b84361e5
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 136679f6596d7e0bf3c33eca51461af13a9fa6d0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="defining-and-identifying-objects-xmla"></a>定义和标识对象 (XMLA)
  在 XML for Analysis (XMLA) 命令中，将使用对象标识符和对象引用标识对象，并使用 Analysis Services 脚本语言 (ASSL) 元素 XMLA 命令定义对象。  
  
## <a name="object-identifiers"></a>对象标识符  
 对象由的实例上的定义使用的对象的唯一标识符标识[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建对象时，可以显式指定对象标识符，也可以由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例确定。 你可以使用[发现](../../analysis-services/xmla/xml-elements-methods-discover.md)方法来检索对象标识符的后续**发现**或[执行](../../analysis-services/xmla/xml-elements-methods-execute.md)方法调用。  
  
## <a name="object-references"></a>对象引用  
 多个 XMLA 命令，如[删除](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)或[过程](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)，对象引用用于明确的方式引用的对象。 对象引用包含要对其执行命令的对象的对象标识符以及该对象的祖先的对象标识符。 例如，分区的对象引用包含分区的对象标识符，以及该分区的父度量值组、多维数据集和数据库的对象标识符。  
  
## <a name="object-definitions"></a>对象定义  
 [创建](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)和[Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) XMLA 中的命令创建或更改，分别对象上[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例。 这些对象的定义都由[ObjectDefinition](../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md)包含从 ASSL 元素的元素。 对象标识符可以通过显式指定所有主要和次要的许多对象使用[ID](../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)元素。 如果**ID**未使用元素，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例提供与取决于要标识的对象的命名约定的唯一标识符。 有关如何使用**创建**和**Alter**命令以定义对象，请参阅[创建和更改对象 &#40;XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md).  
  
## <a name="see-also"></a>另请参阅  
 [Object 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [ParentObject 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)   
 [源元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)   
 [目标元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)   
 [使用 Analysis Services 中的 XMLA 进行开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
