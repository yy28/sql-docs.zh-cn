---
title: 定义和标识对象 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- identifying objects [XML for Analysis]
- XML for Analysis, objects
- object references [XML for Analysis]
- object identifiers [XML for Analysis]
- object definitions [XML for Analysis]
- XMLA, objects
ms.assetid: 43b65f6d-0123-4556-81f0-c7a0b84361e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 595a792e515e862297389faccc324fff8727b8da
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147982"
---
# <a name="defining-and-identifying-objects-xmla"></a>定义和标识对象 (XMLA)
  在 XML for Analysis (XMLA) 命令中，将使用对象标识符和对象引用标识对象，并使用 Analysis Services 脚本语言 (ASSL) 元素 XMLA 命令定义对象。  
  
## <a name="object-identifiers"></a>对象标识符  
 对象标识的实例上定义通过对象的唯一标识符[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建对象时，可以显式指定对象标识符，也可以由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例确定。 可以使用[Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)方法来检索对象标识符的后续`Discover`或[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法调用。  
  
## <a name="object-references"></a>对象引用  
 多个 XMLA 命令，如[删除](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla)或[进程](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)，使用对象引用以明确的方式引用的对象。 对象引用包含要对其执行命令的对象的对象标识符以及该对象的祖先的对象标识符。 例如，分区的对象引用包含分区的对象标识符，以及该分区的父度量值组、多维数据集和数据库的对象标识符。  
  
## <a name="object-definitions"></a>对象定义  
 [创建](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)并[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) XMLA 中的命令创建或更改，分别对象上[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例。 这些对象的定义由[ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla)包含 ASSL 中的元素的元素。 对象标识符可以显式指定的所有主要对象和诸多次要对象通过[ID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)元素。 如果不使用 `ID` 元素，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例将提供一个唯一标识符，其命名约定取决于要标识的对象。 有关如何使用详细信息`Create`并`Alter`命令来定义对象，请参阅[创建和更改对象&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)。  
  
## <a name="see-also"></a>另请参阅  
 [对象元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [ParentObject 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Source 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)   
 [Target 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)   
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
