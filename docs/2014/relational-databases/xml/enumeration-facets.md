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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c326c4f6f9d090d99de00580404953fa242586c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104133"
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
  
## <a name="see-also"></a>请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
