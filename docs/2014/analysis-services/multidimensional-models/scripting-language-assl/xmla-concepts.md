---
title: XMLA 概念 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XMLA, concepts
ms.assetid: 816183a7-d2f7-4e14-8e5b-2a4c1798fbc1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0da9467d293c0081309accd99fb46d7589fb4b8b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62736571"
---
# <a name="xmla-concepts"></a>XMLA 概念
  XML for Analysis (XMLA) 开放标准支持对位于万维网上的数据源的数据访问。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 按 XMLA 1.1 规范实现了 XMLA。  
  
 XML for Analysis (XMLA) 是一种基于简单对象访问协议 (SOAP) 的 XML 协议，它是专为对驻留在 Web 上的任何标准多维数据源的通用数据访问而设计的。 XMLA 还消除了需要部署一个公开组件对象模型 (COM) 的客户端组件或[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 接口。 如果与服务器之间的往返通信要占用大量时间和资源，并且对数据源的有状态连接会限制服务器上的用户连接数，则 XMLA 会针对 Internet 进行优化。  
  
 XMLA 是用于的本机协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，用于客户端应用程序和实例之间的所有交互[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 完全支持 XML for Analysis 1.1，并且还提供了支持元数据管理、会话管理和锁定功能的扩展。 与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例进行通信时，分析管理对象 (AMO) 和 ADOMD.NET 都使用 XMLA 协议。  
  
## <a name="handling-xmla-communications"></a>处理 XMLA 通信  
 XMLA 开放标准介绍了以下两种常规访问方法：`Discover` 和 `Execute`。 这些方法使用 XML 支持的松散耦合客户端和服务器体系结构处理有关 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的传入和传出信息。  
  
 `Discover` 方法可从 Web 服务获取信息和元数据。 此信息可包含可用数据源的列表以及任何数据源访问接口的相关信息。 属性可定义并定形从数据源中获取的数据。 `Discover` 方法是定义多种类型的信息的常用方法，客户端应用程序可能需要从 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的数据源中获取这些信息。 属性和泛型接口可提供可扩展性，而无需重写客户端应用程序中的现有函数。  
  
 `Execute` 方法使应用程序能够对 XMLA 数据源运行特定于访问接口的命令。  
  
 尽管 XMLA 协议是针对 Web 应用程序进行优化的，但它还可用于面向 LAN 的应用程序。 下列应用程序可从基于此 XML 的 API 中获益：  
  
-   需要在客户端与服务器之间使用灵活技术的客户端/服务器应用程序  
  
-   针对多个操作系统的客户端/服务器应用程序  
  
-   不需要明显状态以便增加服务器容量的客户端  
  
## <a name="xmla-and-the-unified-dimensional-model"></a>XMLA 和统一维度模型  
 XMLA 是采用统一维度模型 (UDM) 方法的商业智能应用程序所使用的协议  
  
  
