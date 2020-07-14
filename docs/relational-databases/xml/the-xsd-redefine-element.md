---
title: '&lt;xsd:redefine&gt; 元素 | Microsoft Docs'
description: 了解对 W3C XSD redefine 元素的支持，以及如何更新 XML 架构或其组件。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4f2791ea8a8cae425ae7839a7af2d722e8cfe8a6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729857"
---
# <a name="the-ltxsdredefinegt-element"></a>&lt;xsd:redefine&gt; 元素
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  W3C XSD **redefine** 元素为重新定义架构组件提供了支持。 但是，对此指令的支持可能会严重影响性能，同时还要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新验证与重新定义后的架构关联的 **xml** 数据类型的所有实例。 因此， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持此元素。 服务器拒绝包含 \<xsd:redefine> 元素的 XML 架构。  
  
 若要更新架构或其组件，您可以改为执行以下操作：  
  
1.  用修改后的架构组件创建新的 XML 架构集合。  
  
2.  重新类型化使用要重新定义的 XML 架构集合的所有 **xml** 数据类型 (XML DT)，以便改用新的 XML 架构集合。 为此，请使用 ALTER TABLE 命令的 ALTER COLUMN 选项来重新类型化列，或更改对变量或参数的 XML 架构集合约束。  
  
3.  删除旧版本的 XML 架构集合。  

## <a name="see-also"></a>另请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
