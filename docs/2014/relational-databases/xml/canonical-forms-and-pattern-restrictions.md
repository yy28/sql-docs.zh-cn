---
title: 规范格式和模式限制 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- pattern restrictions
- canonical forms
ms.assetid: 088314ec-7d0b-4a05-8a33-f35da5bfe59c
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d5fb6b52893b4bd79220b1fb6ec5096350f387a7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249697"
---
# <a name="canonical-forms-and-pattern-restrictions"></a>规范格式和模式限制
  XSD 模式方面允许对简单类型的词法空间进行限制。 当把模式限制加在存在多个可能的词法表示形式的类型上时，某些值可能引起对验证的意外行为。  
  
 因为这些值的词法表示形式未存储在数据库中，所以出现此行为。 因此，当这些值作为输出序列化时将其转换为它们的规范表示形式。 如果文档包含的值的规范格式不符合其类型的模式限制，则当用户尝试重新插入该文档时，将拒绝该文档。  
  
 为了避免这种情况， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拒绝任何包含无法重新插入的值的 XML 文档，由于它们的规范格式违反了模式限制。 例如，值“33.000”不对从 **xs:decimal** 派生的带有“33\\.0+”的模式限制的类型进行验证。 尽管“33.000”符合此模式，但规范格式“33”不符合。  
  
 因此，您应时要小心将模式方面应用到从以下基元类型派生的类型： `boolean`， `decimal`， `float`， `double`， `dateTime`， `time`， `date`， `hexBinary`和`base64Binary`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将发出警告。  
  
 浮点值的不精确序列化有类似的问题。 由于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的浮点序列化算法，相似值可能共享相同的规范格式。 当序列化浮点值然后重新插入浮点值时，它的值可能发生轻微变化。 在极个别的情况下，重新插入时这可能导致一个违反其类型的以下任何方面的值： **enumeration**、 **minInclusive**、 **minExclusive**、 **maxInclusive**或 **maxExclusive**。 为了避免这种情况， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拒绝任何从 `xs:float` 或 `xs:double` 派生的类型的值，这些值无法序列化和重新插入。  
  
## <a name="see-also"></a>请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
