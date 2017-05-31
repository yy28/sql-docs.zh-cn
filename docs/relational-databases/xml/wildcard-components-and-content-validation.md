---
title: "通配符组成部分和内容验证 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- wildcard components [XML]
- content validation [XML]
ms.assetid: ffa7d974-3645-446c-8425-f0b22b6b060a
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3eac26ac7add89b64c19672ae9fd34e224c6e7e1
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="wildcard-components-and-content-validation"></a>通配符组成部分和内容验证
  通配符组成部分用于更加灵活地在内容模型中显示内容。 在 XSD 语言中按照以下方式支持这些组成部分：  
  
-   元素通配符组成部分。 这些组成部分通过 **\<xsd:any>** 元素表示。  
  
-   属性通配符组成部分。 这些组成部分通过 **\<xsd:anyAttribute>** 元素表示。  
  
 这两个通配符元素（**\<xsd:any>** 和 **\<xsd:anyAttribute>**）都支持 **processContents** 属性的使用。 这将允许您指定特定的值，该值指示 XML 应用程序如何处理与这些通配符元素关联的文档内容的验证。 以下是不同的值及其作用：  
  
-   **strict** 值指定对内容进行完整的验证。  
  
-   **skip** 值指定不对内容进行验证。  
  
-   **lax** 值指定仅对具有可用架构定义的元素和属性进行验证。  
  
## <a name="lax-validation-and-xsanytype-elements"></a>宽松验证与 xs:anyType 元素  
 XML 架构规范对 **anyType** 类型的元素进行 **宽松** 验证。 因为 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 不支持宽松验证，所以对 **anyType**类型的元素进行严格验证。 从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]开始，支持宽松验证。 **anyType** 类型的元素的内容将使用宽松验证方式进行验证。  
  
 下面的示例说明了宽松验证。 架构元素 `e` 属于 **anyType** 类型。 此示例创建了类型化的 **xml** 变量并说明了 **anyType** 类型的元素的宽松验证。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="http://ns">  
   <element name="e" type="anyType"/>  
   <element name="a" type="byte"/>  
   <element name="b" type="string"/>  
 </schema>'  
GO  
```  
  
 下面的示例将成功执行，因为 `<e>` 的验证会成功：  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><b>data</b></e>'  
GO  
```  
  
 下面的示例将成功执行。 尽管架构中未定义 `<c>` 元素，仍会接受此实例：  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><c>Wrong</c><b>data</b></e>'  
GO  
```  
  
 下面的示例中的 XML 实例将被拒绝，原因是 `<a>` 元素的定义不允许使用字符串值。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>Wrong</a><b>data</b></e>'  
SELECT @var  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
