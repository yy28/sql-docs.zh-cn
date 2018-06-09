---
title: XML for Analysis (XMLA) 参考 |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e8c3645175d8d1f3251fd621825f5a542669cbb
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34576759"
---
# <a name="xml-for-analysis--xmla-reference"></a>XML for Analysis (XMLA) 引用
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]   

Azure Analysis Services 和 SQL Server Analysis Services 将 XML 用于 Analysis (XMLA) 协议客户端应用程序和 Analysis Services 实例之间进行通信。 在通信的最基本一级，其他客户端库（如 ADOMD.NET 和 AMO）采用 XMLA 构造请求并对响应解码，充当完全使用 XMLA 的 Analysis Services 实例的中介。  
  
 若要在表格和多维模式下支持的发现和操作数据，XMLA 规范定义了两个通常访问的方法，[发现](../../analysis-services/xmla/xml-elements-methods-discover.md)和[执行](../../analysis-services/xmla/xml-elements-methods-execute.md)，和一个XML 元素和数据类型的集合。 由于 XML 可用于松散耦合客户端和服务器体系结构，因此这两种方法都可处理 XML 格式的传入和传出信息。 

Analysis Services 符合 XMLA 1.1 规范中，但也使之包括数据定义和操作功能，在上以批注的形式实现了扩展**发现**和**执行**方法。 扩展的 XML 语法是表格模型脚本语言 (TMSL) 和 Analysis Services 脚本语言 (ASSL)。 

TMSL 是兼容级别 1200年或更高的表格模型数据库的命令和对象模型定义语法。 TMSL 与 Analysis Services 通信通过 XMLA 协议，其中`XMLA.Execute`方法接受采用 TMSL 这两个基于 JSON 的语句脚本以及 Analysis Services 脚本语言 (的 XMLA ASSL) 中的传统的基于 XML 的脚本。 若要了解详细信息，请参阅[表格模型脚本语言 (TMSL) 参考](../tabular-model-scripting-language-tmsl-reference.md)。

ASSL 是多维模型数据库和兼容级别 1103年或更低的表格模式下数据库的命令和对象的模型定义语法。 此定义而不会破坏其基于 XMLA 规范。 不管您单独使用 XMLA 还是结合使用 XMLA 和 ASSL，都确保基于 XMLA 的互操作性。 若要了解详细信息，请参阅[Analysis Services 脚本语言 (的 XMLA ASSL)](../scripting/analysis-services-scripting-language-assl-for-xmla.md)。
  
 作为开发人员，你可以使用 XMLA 作为接口如果解决方案要求指定标准协议，如 XML、 SOAP 和 HTTP。 开发人员和管理员还可用于 XMLA 临时地从服务器检索信息或运行命令。 
  
## <a name="in-this-section"></a>在本节中  
  
|主题|Description|  
|-----------|-----------------|  
|[XML 数据类型 (XMLA)](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)|介绍 XMLA 规范中的数据类型。|  
|[XML 元素的命令 (XMLA)](../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)|Execute 方法调用期间可使用命令元素内的元素。|  
|[XML 元素的命令 (XMLA)](../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)|Execute 方法调用期间可使用命令元素内的元素。|  
|[XML 元素-标头 (XMLA)](../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)| 标头实现 Microsoft Analysis Services 的元素。|  
|[XML 元素的属性 (XMLA)](../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)| 用于表示属性信息和 XMLA 标头、 方法、 对象、 命令和数据类型值的元素。|  
|[XML 元素的方法的发现 (XMLA)](../../analysis-services/xmla/xml-elements-methods-discover.md)| 从 Analysis Services 的实例中检索信息，如可用数据库或针对特定对象的详细信息的列表。|  
|[XML 元素的方法的执行 (XMLA)](../../analysis-services/xmla/xml-elements-methods-execute.md)| 将 XML Analysis (XMLA) 命令发送到的 Analysis Services 实例。|  
|[XML 元素的对象-DiscoverResponse (XMLA)](../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)| 包含返回到发现方法调用的响应中的 Analysis Services 实例的信息。|  
|[XML 元素的对象-ExecuteResponse (XMLA)](../../analysis-services/xmla/xml-elements-objects-executeresponse.md)| 包含返回响应的 Execute 方法调用中的 Analysis Services 实例的信息。|  
|[XML 元素的对象 (XMLA)](../../analysis-services/xmla/xml-elements-objects.md)| Analysis services 中实现的对象。|  
|[XML for Analysis 符合性 (XMLA)](../../analysis-services/xmla/xml-for-analysis-compliance-xmla.md)|说明与 XMLA 1.1 规范遵从的级别。|  
  
## <a name="see-also"></a>另请参阅
 [XML for Analysis 架构行集](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
 [使用 ADOMD.NET 进行开发](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
 [使用分析管理对象 (AMO) 进行开发](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
