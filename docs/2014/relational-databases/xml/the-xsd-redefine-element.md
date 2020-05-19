---
title: '&lt;xsd:redefine&gt; 元素 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 59eafff14c6a0cc7752817a31648b64bd5edc907
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702451"
---
# <a name="the-ltxsdredefinegt-element"></a>&lt;xsd:redefine&gt; 元素
  W3C XSD **redefine** 元素为重新定义架构组件提供了支持。 但是，对此指令的支持可能会导致性能高昂，同时还要求重新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 验证与重新 `xml` 定义的架构关联的数据类型的所有实例。 因此， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持此元素。 服务器拒绝包含 **\<xsd:redefine>** 元素的 XML 架构。  
  
 若要更新架构或其组件，您可以改为执行以下操作：  
  
1.  用修改后的架构组件创建新的 XML 架构集合。  
  
2.  重新键入 `xml` 使用要重新定义的 Xml 架构集合的所有数据类型（XML DT），以便改用新的 Xml 架构集合。 为此，请使用 ALTER TABLE 命令的 ALTER COLUMN 选项来重新类型化列，或更改对变量或参数的 XML 架构集合约束。  
  
3.  删除旧版本的 XML 架构集合。  
  
## <a name="see-also"></a>另请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
