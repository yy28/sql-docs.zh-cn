---
title: "XML for Analysis (XMLA) 参考 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- XML for Analysis, reference
- XMLA, reference
ms.assetid: 88045e05-ce47-4e28-999b-7f9c74af9faf
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 826536d6f28df078b3ca0899176303cbe1a06865
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="xml-for-analysis--xmla-reference"></a>XML for Analysis (XMLA) 引用
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XML for Analysis (XMLA) 协议用于处理客户端应用程序和 Analysis Services 实例之间的所有通信。 在通信的最基本一级，其他客户端库（如 ADOMD.NET 和 AMO）采用 XMLA 构造请求并对响应解码，充当完全使用 XMLA 的 Analysis Services 实例的中介。  
  
 若要在多维和表格格式支持发现和操作数据，XMLA 规范定义了两个通常访问的方法，[发现](../../analysis-services/xmla/xml-elements-methods-discover.md)和[执行](../../analysis-services/xmla/xml-elements-methods-execute.md)，和一个XML 元素和数据类型的集合。 由于 XML 可用于松散耦合客户端和服务器体系结构，因此这两种方法都可处理 XML 格式的传入和传出信息。 Analysis Services 符合 XMLA 1.1 规范中，但也使之包括数据定义和操作功能，在上以批注的形式实现了扩展**发现**和**执行**方法。 扩展的 XML 语法被称为 Analysis Services 脚本语言 (ASSL)。 ASSL 构建在 XMLA 规范之上并且完全符合该规范。 不管您单独使用 XMLA 还是结合使用 XMLA 和 ASSL，都确保基于 XMLA 的互操作性。  
  
 作为编程人员，如果解决方案要求指定标准协议（如 XML、SOAP 和 HTTP），则您可以将 XMLA 用作编程接口。 编程人员和管理员还可以按需使用 XMLA 从服务器检索信息或运行命令。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[XML 元素 &#40;XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)|介绍 XMLA 规范中的元素。|  
|[XML 数据类型 &#40;XMLA &#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)|介绍 XMLA 规范中的数据类型。|  
|[XML for Analysis 遵从性 &#40;XMLA &#41;](../../analysis-services/xmla/xml-for-analysis-compliance-xmla.md)|说明与 XMLA 1.1 规范遵从的级别。|  
  
## <a name="related-sections"></a>相关章节  
 [使用 Analysis Services 脚本语言 (ASSL) 开发](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
  
 [XML for Analysis 架构行集](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 [使用 ADOMD.NET 进行开发](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
 [使用分析管理对象 (AMO) 进行开发](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
  
## <a name="see-also"></a>另请参阅  
 [了解 Microsoft OLAP 体系结构](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
