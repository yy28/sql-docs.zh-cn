---
title: 枚举方面 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- enumeration facets
ms.assetid: dec23a79-ddd6-4701-9721-55a2c435a34d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bdc9f1f8ce97941d111cd187b4228fd498fbfe8c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716969"
---
# <a name="enumeration-facets"></a>枚举方面
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拒绝包含以下类型的 XML 架构：具有模式方面或违反这些方面的枚举的类型。  
  
## <a name="example"></a>示例  
 下面的架构将会被拒绝，因为主要枚举值包含大小写混合的值。 此值违反了将值限制为只包含小写字母的模式值，从这一点来说，它也会被拒绝。  
  
```  
CREATE XML SCHEMA COLLECTION MySampleCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
    <simpleType name="MyST">  
       <restriction base="string">  
          <pattern value="[a-z]*"/>  
       </restriction>  
    </simpleType>  
  
    <simpleType name="MyST2">  
       <restriction base="ns:MyST">  
           <enumeration value="mYstring"/>  
       </restriction>  
    </simpleType>  
</schema>'  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
