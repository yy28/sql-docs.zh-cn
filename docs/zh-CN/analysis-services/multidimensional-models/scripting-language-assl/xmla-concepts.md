---
title: XMLA 概念 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 429d1bc09714d15cfb8fbd851c72e01dd8ba198b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="xmla-concepts"></a>XMLA 概念
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  XML for Analysis (XMLA) 开放标准支持对位于万维网上的数据源的数据访问。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 每个 XMLA 1.1 规范实现 XMLA。  
  
 XML for Analysis (XMLA) 是一种基于简单对象访问协议 (SOAP) 的 XML 协议，它是专为对驻留在 Web 上的任何标准多维数据源的通用数据访问而设计的。 XMLA 还消除了需部署公开组件对象模型 (COM) 的客户端组件或[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 接口。 如果与服务器之间的往返通信要占用大量时间和资源，并且对数据源的有状态连接会限制服务器上的用户连接数，则 XMLA 会针对 Internet 进行优化。  
  
 XMLA 是用于的本机协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，用于客户端应用程序的实例之间的所有交互[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 完全支持 XML for Analysis 1.1，并且还提供了支持元数据管理、会话管理和锁定功能的扩展。 与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例进行通信时，分析管理对象 (AMO) 和 ADOMD.NET 都使用 XMLA 协议。  
  
## <a name="handling-xmla-communications"></a>处理 XMLA 通信  
 XMLA 开放标准介绍两种通常可访问的方法：**发现**和**执行**。 这些方法使用 XML 支持的松散耦合客户端和服务器体系结构处理有关 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的传入和传出信息。  
  
 **发现**方法从 Web 服务获取信息和元数据。 此信息可包含可用数据源的列表以及任何数据源访问接口的相关信息。 属性可定义并定形从数据源中获取的数据。 **发现**方法是用于定义多种类型的客户端应用程序可能需要从数据源的信息的常见方法[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。 属性和泛型接口可提供可扩展性，而无需重写客户端应用程序中的现有函数。  
  
 **执行**方法允许应用程序针对 XMLA 数据源运行特定于提供程序的命令。  
  
 尽管 XMLA 协议是针对 Web 应用程序进行优化的，但它还可用于面向 LAN 的应用程序。 下列应用程序可从基于此 XML 的 API 中获益：  
  
-   需要在客户端与服务器之间使用灵活技术的客户端/服务器应用程序  
  
-   针对多个操作系统的客户端/服务器应用程序  
  
-   不需要明显状态以便增加服务器容量的客户端  
  
## <a name="xmla-and-the-unified-dimensional-model"></a>XMLA 和统一维度模型  
 XMLA 是采用统一维度模型 (UDM) 方法的商业智能应用程序所使用的协议  
  
  
