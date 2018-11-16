---
title: 不确定性内容模型 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- non-deterministic content models
- content models [XML in SQL Server]
ms.assetid: 9d4513e7-dd19-4491-b7c7-28bc7c2f8589
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6ef6f0f0a8d271780df238f9af175d4a85df7297
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51656459"
---
# <a name="non-deterministic-content-models"></a>不确定性内容模型
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 (SP1) 之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拒绝包含不确定性内容模型的 XML 架构。  
  
 不过从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1 开始，如果匹配项约束为 0、1 或不受限制，则会接受不确定性内容模型。  
  
## <a name="example-non-deterministic-content-model-rejected"></a>示例：拒绝的不确定性内容模型  
 下面的示例尝试创建具有不确定的内容模型的 XML 架构。 此代码失败，因为不清楚 `<root>` 元素应有一个包含两个 `<a>` 元素的序列，还是 `<root>` 元素应有两个序列，其中每个序列有一个 `<a>` 元素。  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="https://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="1" maxOccurs="2">  
                <element name="a" type="string" minOccurs="1" maxOccurs="2"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
 可以通过将匹配项约束移动到一个唯一的位置来修复此架构。 例如，可以将此约束移动到包含序列粒子：  
  
```  
<sequence minOccurs="1" maxOccurs="4">  
    <element name="a" type="string" minOccurs="1" maxOccurs="1"/>  
</sequence>  
```  
  
 也可以将此约束移动到被包含元素：  
  
```  
<sequence minOccurs="1" maxOccurs="1">  
     <element name="a" type="string" minOccurs="1" maxOccurs="4"/>  
</sequence>  
```  
  
## <a name="example-non-deterministic-content-model-accepted"></a>示例：接受的不确定性内容模型  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SP1 之前的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 版本中，会拒绝下面的架构。  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="https://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="0" maxOccurs="unbounded">  
                <element name="a" type="string" minOccurs="0" maxOccurs="1"/>  
                <element name="b" type="string" minOccurs="1" maxOccurs="unbounded"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
