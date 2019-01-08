---
title: Analysis Services 数据挖掘编程 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 27a964581782d5868e4089a1063dbbce0c689525
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072754"
---
# <a name="data-mining-programming"></a>数据挖掘编程
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  如果您觉得 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的内置工具和查看器不符合您的要求，您可以编写自己的扩展插件代码来扩展 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的功能。 如果采用这种方法，您有两种选择：  
  
-   **XMLA**  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持 XML for Analysis (XMLA) 作为与客户端应用程序进行通信协议。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 还支持其他扩展了 XML for Analysis 规范的命令。  
  
     由于 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将 XMLA 用于数据定义、数据操作和数据控制支持，因此您可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供的可视化工具创建挖掘结构和挖掘模型，然后扩展已使用数据挖掘扩展插件 (DMX) 和 Analysis Services 脚本语言 (ASSL) 脚本创建的数据挖掘对象。  
  
     您可以创建和修改 XMLA 脚本中的全部数据挖掘对象，并以编程方式从您自己的应用程序对模型运行预测查询。  
  
-   **分析管理对象 (AMO)**  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 还提供了一个完整的框架，该框架使第三方数据挖掘访问接口能够将数据挖掘对象集成到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中。  
  
     可以使用 AMO 创建挖掘结构和挖掘模型。 在 CodePlex 中查看以下示例：  
  
    -   AMO 浏览器  
  
         连接到您指定的 SSAS 实例，并列出所有服务器对象及其属性（包括挖掘结构和挖掘模型）。  
  
    -   AMO 简单示例  
  
         AS 简单示例涉及对大多数主要对象的编程访问，并演示元数据浏览以及对象中的值的访问。  
  
         该示例还演示如何创建和处理数据挖掘结构和模型，以及浏览现有数据挖掘模型。  
  
-   **DMX**  
  
     您可以使用 DMX 封装命令语句、预测查询和元数据查询并以表格格式返回结果（假定您创建了与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器的连接）。  
  
## <a name="in-this-section"></a>本节内容  
 [数据挖掘 OLE DB](../analysis-services/data-mining-programming-ole-db.md)  
 介绍在支持数据挖掘和多维数据方面对规范的扩展：新的架构行集和列，以及用于创建和管理挖掘结构的数据挖掘扩展插件 (DMX) 语言。  
  
## <a name="related-reference"></a>相关参考  
 [使用 ADOMD.NET 进行开发](../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
 介绍 ADOMD.NET 客户端和服务器编程对象。  
  
 [使用分析管理对象 (AMO) 进行开发](../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
 介绍 AMO 编程库。  
  
 [使用 Analysis Services 脚本语言 (ASSL) 开发](../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
 介绍 XML for Analysis (XMLA) 及其扩展插件。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 开发人员文档](../analysis-services/analysis-services-developer-documentation.md)   
 [数据挖掘扩展插件 (DMX) 参考](../dmx/data-mining-extensions-dmx-reference.md)  
  
  
