---
title: 定义和标识对象（XMLA） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: ad6c8de47577eccd7797517c8080957d7afe1abd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62727540"
---
# <a name="defining-and-identifying-objects-xmla"></a>定义和标识对象 (XMLA)
  在 XML for Analysis (XMLA) 命令中，将使用对象标识符和对象引用标识对象，并使用 Analysis Services 脚本语言 (ASSL) 元素 XMLA 命令定义对象。  
  
## <a name="object-identifiers"></a>对象标识符  
 对象通过使用在的实例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]上定义的对象的唯一标识符进行标识。 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建对象时，可以显式指定对象标识符，也可以由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例确定。 可以使用[发现](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)方法检索对象标识符，以便执行后续`Discover`或[执行](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法调用。  
  
## <a name="object-references"></a>对象引用  
 一些 XMLA 命令（如[删除](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla)或[处理](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)）使用对象引用以明确的方式引用对象。 对象引用包含要对其执行命令的对象的对象标识符以及该对象的祖先的对象标识符。 例如，分区的对象引用包含分区的对象标识符，以及该分区的父度量值组、多维数据集和数据库的对象标识符。  
  
## <a name="object-definitions"></a>对象定义  
 XMLA 中的[create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)和[alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)命令分别创建或更改[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例上的对象。 这些对象的定义由包含 ASSL 元素的[ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla)元素表示。 可以通过使用[ID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)元素为所有主要和多个次要对象显式指定对象标识符。 如果不使用 `ID` 元素，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例将提供一个唯一标识符，其命名约定取决于要标识的对象。 有关如何使用`Create`和`Alter`命令定义对象的详细信息，请参阅[&#40;XMLA&#41;创建和更改对象](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;XMLA&#41;的对象元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [&#40;XMLA&#41;的 ParentObject 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [&#40;XMLA&#41;源元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)   
 [&#40;XMLA&#41;的目标元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)   
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
