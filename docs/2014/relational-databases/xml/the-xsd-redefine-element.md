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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e9fa3dedafc05406dcc521429130f98a215d294
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62679967"
---
# <a name="the-ltxsdredefinegt-element"></a>&lt;xsd:redefine&gt; 元素
  W3C XSD **redefine** 元素为重新定义架构组件提供了支持。 但是，对此指令可能会严重影响性能，同时还要求的支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新进行验证的所有实例`xml`重新定义的架构与相关联的数据类型。 因此， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持此元素。 服务器拒绝包含 **\<xsd:redefine>** 元素的 XML 架构。  
  
 若要更新架构或其组件，您可以改为执行以下操作：  
  
1.  用修改后的架构组件创建新的 XML 架构集合。  
  
2.  重新键入所有`xml`使用 XML 架构集合重新定义以改为使用新的 XML 架构集合的数据类型 (XML DT)。 为此，请使用 ALTER TABLE 命令的 ALTER COLUMN 选项来重新类型化列，或更改对变量或参数的 XML 架构集合约束。  
  
3.  删除旧版本的 XML 架构集合。  
  
## <a name="see-also"></a>请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
