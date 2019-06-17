---
title: 数据挖掘编程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- data mining [Analysis Services], developer's guide
ms.assetid: 9fd77b16-0b89-44ce-bcf1-7c04b62499da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9d18e97a60bf1c6108b3672f40747e8b612ad6e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62732220"
---
# <a name="data-mining-programming"></a>数据挖掘编程
  如果您觉得 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的内置工具和查看器不符合您的要求，您可以编写自己的扩展插件代码来扩展 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的功能。 如果采用这种方法，您有两种选择：  
  
-   **XMLA**  
  
     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 支持 XML for Analysis (XMLA) 作为与客户端应用程序进行通信协议。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还支持其他扩展了 XML for Analysis 规范的命令。  
  
     由于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将 XMLA 用于数据定义、数据操作和数据控制支持，因此您可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 提供的可视化工具创建挖掘结构和挖掘模型，然后扩展已使用数据挖掘扩展插件 (DMX) 和 Analysis Services 脚本语言 (ASSL) 脚本创建的数据挖掘对象。  
  
     您可以创建和修改 XMLA 脚本中的全部数据挖掘对象，并以编程方式从您自己的应用程序对模型运行预测查询。  
  
-   **分析管理对象 (AMO)**  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还提供了一个完整的框架，该框架使第三方数据挖掘访问接口能够将数据挖掘对象集成到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中。  
  
     可以使用 AMO 创建挖掘结构和挖掘模型。 在 CodePlex 中查看以下示例：  
  
    -   AMO 浏览器  
  
         连接到您指定的 SSAS 实例，并列出所有服务器对象及其属性（包括挖掘结构和挖掘模型）。  
  
    -   AMO 简单示例  
  
         AS 简单示例涉及对大多数主要对象的编程访问，并演示元数据浏览以及对象中的值的访问。  
  
         该示例还演示如何创建和处理数据挖掘结构和模型，以及浏览现有数据挖掘模型。  
  
-   **DMX**  
  
     您可以使用 DMX 封装命令语句、预测查询和元数据查询并以表格格式返回结果（假定您创建了与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器的连接）。  
  
## <a name="in-this-section"></a>本节内容  
 [数据挖掘 OLE DB](../../../2014/analysis-services/dev-guide/ole-db-for-data-mining.md)  
 介绍在支持数据挖掘和多维数据方面对规范的扩展：新的架构行集和列，以及用于创建和管理挖掘结构的数据挖掘扩展插件 (DMX) 语言。  
  
## <a name="related-reference"></a>相关参考  
 [使用 ADOMD.NET 进行开发](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net)  
 介绍 ADOMD.NET 客户端和服务器编程对象。  
  
 [使用分析管理对象 (AMO) 进行开发](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)  
 介绍 AMO 编程库。  
  
 [使用 Analysis Services 脚本语言 (ASSL) 开发](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
 介绍 XML for Analysis (XMLA) 及其扩展插件。  
  
## <a name="see-also"></a>请参阅  
 [开发人员指南&#40;Analysis Services&#41;](../analysis-services-developer-documentation.md)   
 [数据挖掘扩展插件 (DMX) 参考](/sql/dmx/data-mining-extensions-dmx-reference)  
  
  
