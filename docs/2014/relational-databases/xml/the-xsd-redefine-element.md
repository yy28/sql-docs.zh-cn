---
title: '&lt;xsd:redefine&gt; 元素 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4ca94410d7011c30de0a5481451337d11fa57120
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36139012"
---
# <a name="the-ltxsdredefinegt-element"></a>&lt;xsd:redefine&gt; 元素
  W3C XSD **redefine** 元素为重新定义架构组件提供了支持。 但是，对此指令的可能会严重影响性能，并且还要求支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新验证的所有实例`xml`与重新定义架构关联的数据类型。 因此， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持此元素。 服务器拒绝包含 **\<xsd:redefine>** 元素的 XML 架构。  
  
 若要更新架构或其组件，您可以改为执行以下操作：  
  
1.  用修改后的架构组件创建新的 XML 架构集合。  
  
2.  重新类型化使用要重新定义的 XML 架构集合的所有 `xml` 数据类型 (XML DT)，以便改用新的 XML 架构集合。 为此，请使用 ALTER TABLE 命令的 ALTER COLUMN 选项来重新类型化列，或更改对变量或参数的 XML 架构集合约束。  
  
3.  删除旧版本的 XML 架构集合。  
  
## <a name="see-also"></a>请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  