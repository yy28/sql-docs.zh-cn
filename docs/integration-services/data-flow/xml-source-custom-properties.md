---
title: XML 源自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bfad67095446d9a5143a4262f05520f76ff96dfe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778435"
---
# <a name="xml-source-custom-properties"></a>XML 源自定义属性
  XML 源具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍 XML 源的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|用来访问 XML 数据的模式。|  
|UseInlineSchema|Boolean|该值指示是否要在 XML 源中使用内联架构定义。 此属性的默认值为 **False**。|  
|XMLData|String|要从中检索 XML 数据的文件或变量。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
|XMLSchemaDefinition|String|架构定义文件 (.xsd) 的路径和文件名。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
  
 下表描述了 XML 源的输出的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|RowsetID|String|标识与输出关联的行集的值。|  
  
 XML 源的输出列没有自定义属性。  
  
 有关详细信息，请参阅 [XML Source](../../integration-services/data-flow/xml-source.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
