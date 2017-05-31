---
title: "&lt;xsd:redefine&gt; 元素 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 74822cb1a24319e1926866da283b1ada379709e8
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="the-ltxsdredefinegt-element"></a>&lt;xsd:redefine&gt; 元素
  W3C XSD **redefine** 元素为重新定义架构组件提供了支持。 但是，对此指令的支持可能会严重影响性能，同时还要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新验证与重新定义后的架构关联的 **xml** 数据类型的所有实例。 因此， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持此元素。 服务器拒绝包含 **\<xsd:redefine>** 元素的 XML 架构。  
  
 若要更新架构或其组件，您可以改为执行以下操作：  
  
1.  用修改后的架构组件创建新的 XML 架构集合。  
  
2.  重新类型化使用要重新定义的 XML 架构集合的所有 **xml** 数据类型 (XML DT)，以便改用新的 XML 架构集合。 为此，请使用 ALTER TABLE 命令的 ALTER COLUMN 选项来重新类型化列，或更改对变量或参数的 XML 架构集合约束。  
  
3.  删除旧版本的 XML 架构集合。  
  
## <a name="see-also"></a>另请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
