---
title: "规范格式和模式限制 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pattern restrictions
- canonical forms
ms.assetid: 088314ec-7d0b-4a05-8a33-f35da5bfe59c
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a20cb4d1a23ed32f7bddf1aa79d5428f46b9926e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="canonical-forms-and-pattern-restrictions"></a>规范格式和模式限制
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]XSD 模式方面允许对简单类型的词法空间进行限制。 当把模式限制加在存在多个可能的词法表示形式的类型上时，某些值可能引起对验证的意外行为。  
  
 因为这些值的词法表示形式未存储在数据库中，所以出现此行为。 因此，当这些值作为输出序列化时将其转换为它们的规范表示形式。 如果文档包含的值的规范格式不符合其类型的模式限制，则当用户尝试重新插入该文档时，将拒绝该文档。  
  
 为了避免这种情况， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拒绝任何包含无法重新插入的值的 XML 文档，由于它们的规范格式违反了模式限制。 例如，值“33.000”不对从 **xs:decimal** 派生的带有“33\\.0+”的模式限制的类型进行验证。 尽管“33.000”符合此模式，但规范格式“33”不符合。  
  
 因此，将模式方面应用到从以下基元类型派生的类型时应当小心： **boolean**、 **decimal**、 **float**、 **double**、 **dateTime**、 **time**、 **date**、 **hexBinary**和 **base64Binary**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将发出警告。  
  
 浮点值的不精确序列化有类似的问题。 由于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的浮点序列化算法，相似值可能共享相同的规范格式。 当序列化浮点值然后重新插入浮点值时，它的值可能发生轻微变化。 在极个别的情况下，重新插入时这可能导致一个违反其类型的以下任何方面的值： **enumeration**、 **minInclusive**、 **minExclusive**、 **maxInclusive**或 **maxExclusive**。 为了避免这种情况， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拒绝任何从 `xs:float` 或 `xs:double` 派生的类型的值，这些值无法序列化和重新插入。  
  
## <a name="see-also"></a>另请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
