---
title: XML 源自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e5c992253304d2a1c493f52a9e24cf569ff29883
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392725"
---
# <a name="xml-source-custom-properties"></a>XML 源自定义属性
  XML 源具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍 XML 源的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|用来访问 XML 数据的模式。|  
|UseInlineSchema|Boolean|该值指示是否要在 XML 源中使用内联架构定义。 此属性的默认值为 `False`。|  
|XMLData|String|要从中检索 XML 数据的文件或变量。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
|XMLSchemaDefinition|String|架构定义文件 (.xsd) 的路径和文件名。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
  
 下表描述了 XML 源的输出的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|RowsetID|String|标识与输出关联的行集的值。|  
  
 XML 源的输出列没有自定义属性。  
  
 有关详细信息，请参阅 [XML Source](xml-source.md)。  
  
## <a name="see-also"></a>请参阅  
 [Common Properties](../common-properties.md)  
  
  
