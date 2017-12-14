---
title: "XML 源自定义属性 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 71715e49538a68100b73a7a7fe310db9a17386d1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="xml-source-custom-properties"></a>XML 源自定义属性
  XML 源具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍 XML 源的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|用来访问 XML 数据的模式。|  
|UseInlineSchema|Boolean|该值指示是否要在 XML 源中使用内联架构定义。 此属性的默认值为 **False**。|  
|XMLData|字符串|要从中检索 XML 数据的文件或变量。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
|XMLSchemaDefinition|字符串|架构定义文件 (.xsd) 的路径和文件名。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
  
 下表描述了 XML 源的输出的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|RowsetID|字符串|标识与输出关联的行集的值。|  
  
 XML 源的输出列没有自定义属性。  
  
 有关详细信息，请参阅 [XML Source](../../integration-services/data-flow/xml-source.md)。  
  
## <a name="see-also"></a>另请参阅  
 [通用属性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
