---
title: XML for Analysis (XMLA) 参考 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, reference
- XMLA, reference
ms.assetid: 88045e05-ce47-4e28-999b-7f9c74af9faf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fde04360c7b6af1c9bf6aa906328e5031eb76c32
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164437"
---
# <a name="xml-for-analysis--xmla-reference"></a>XML for Analysis (XMLA) 参考
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用 XML for Analysis (XMLA) 协议处理客户端应用程序和 Analysis Services 实例之间的所有通信。 在通信的最基本一级，其他客户端库（如 ADOMD.NET 和 AMO）采用 XMLA 构造请求并对响应解码，充当完全使用 XMLA 的 Analysis Services 实例的中介。  
  
 若要在多维和表格格式支持的发现和数据操作，XMLA 规范定义了两种常规访问方法[Discover](xml-elements-methods-discover.md)并[Execute](xml-elements-methods-execute.md)，和一个XML 元素和数据类型的集合。 由于 XML 可用于松散耦合客户端和服务器体系结构，因此这两种方法都可处理 XML 格式的传入和传出信息。 Analysis Services 符合 XMLA 1.1 规范，但也对其进行了扩展，可包括数据定义和操作功能（作为 `Discover` 和 `Execute` 方法的批注实现）。 扩展的 XML 语法被称为 Analysis Services 脚本语言 (ASSL)。 ASSL 构建在 XMLA 规范之上并且完全符合该规范。 不管您单独使用 XMLA 还是结合使用 XMLA 和 ASSL，都确保基于 XMLA 的互操作性。  
  
 作为编程人员，如果解决方案要求指定标准协议（如 XML、SOAP 和 HTTP），则您可以将 XMLA 用作编程接口。 编程人员和管理员还可以按需使用 XMLA 从服务器检索信息或运行命令。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[XML 元素&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)|介绍 XMLA 规范中的元素。|  
|[XML 数据类型&#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)|介绍 XMLA 规范中的数据类型。|  
|[XML for Analysis 遵从性&#40;XMLA&#41;](xml-for-analysis-compliance-xmla.md)|说明与 XMLA 1.1 规范遵从的级别。|  
  
## <a name="related-sections"></a>相关章节  
 [开发使用 Analysis Services 脚本语言&#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
  
 [XML for Analysis 架构行集](../schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 [使用 ADOMD.NET 进行开发](../multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
 [使用分析管理对象开发&#40;AMO&#41;](../multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
  
## <a name="see-also"></a>请参阅  
 [了解 Microsoft OLAP 体系结构](../multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
