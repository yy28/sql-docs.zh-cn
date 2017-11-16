---
title: "使用 ADOMD.NET 开发 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET
ms.assetid: abaf33aa-db55-43bf-8f30-15547559be1d
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e0c9a2e2e2bc0b5900beeb65d4b80fdfc61fafb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="developing-with-adomdnet"></a>使用 ADOMD.NET 进行开发
  ADOMD.NET 是[!INCLUDE[msCoName](../../../includes/msconame-md.md)]旨在与进行通信的.NET Framework 数据提供程序[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 ADOMD.NET 可使用 XML for Analysis 协议与分析数据源通信，方法为使用 TCP/IP 或 HTTP 连接传输和接收符合 XML for Analysis 规范的 SOAP 请求和响应。 命令可通过多维表达式 (MDX)、数据挖掘扩展插件 (DMX)、Analysis Services 脚本语言 (ASSL) 或者甚至是有限 SQL 语法来发送，并且可能不返回结果。 可以使用 ADOMD.NET 对象模型来查询和操作分析数据、关键绩效指标 (KPI) 和挖掘模型。 使用 ADOMD.NET 时，还可通过检索与 OLE DB 兼容的架构行集或者使用 ADOMD.NET 对象模型来查看和使用元数据。  
  
 ADOMD.NET 数据访问接口都由**Microsoft.AnalysisServices.AdomdClient**命名空间。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[ADOMD.NET 客户端编程](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)|介绍如何使用 ADOMD.NET 客户端对象从分析数据源检索数据和元数据。|  
|[ADOMD.NET Server 编程](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)|介绍如何使用 ADOMD.NET 服务器对象创建存储过程和用户定义函数。|  
|[重新分发 ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/redistributing-adomd-net.md)|介绍重新发布 ADOMD.NET 的过程。|  
|<xref:Microsoft.AnalysisServices.AdomdClient>|详细信息中包含的对象**Microsoft.AnalysisServices.AdomdClient**命名空间。|  
  
## <a name="see-also"></a>另请参阅  
 [多维表达式 &#40;MDX &#41;引用](../../../mdx/multidimensional-expressions-mdx-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;引用](../../../dmx/data-mining-extensions-dmx-reference.md)   
 [Analysis Services 架构行集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [使用 Analysis Services 脚本语言 &#40; 进行开发ASSL &#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [多维模型数据访问 &#40;Analysis Services-多维数据 &#41;](../../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)  
  
  

