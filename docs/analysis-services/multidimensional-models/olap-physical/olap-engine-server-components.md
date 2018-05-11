---
title: OLAP 引擎服务器组件 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a2fd28f4f9c901759ef672094299b60645dfc763
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="olap-engine-server-components"></a>OLAP 引擎服务器组件
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  服务器组件[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]是**msmdsrv.exe**作为 Windows 服务运行的应用程序。 该应用程序包含安全组件、一个 XML for Analysis (XMLA) 侦听器组件、一个查询处理器组件以及执行下列功能的多个其他内部组件：  
  
-   分析从客户端接收的语句  
  
-   管理元数据  
  
-   处理翻译  
  
-   处理计算  
  
-   存储维度和单元数据  
  
-   创建聚合  
  
-   计划查询  
  
-   缓存对象  
  
-   管理服务器资源  
  
## <a name="architectural-diagram"></a>体系结构关系图  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例作为独立的服务来运行，与该服务的通信使用 HTTP 或 TCP 通过 XML for Analysis (XMLA) 进行。 AMO 是用户应用程序和 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例之间的一层。 这一层提供对 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 管理对象的访问。 AMO 是一个类库，它从客户端应用程序获取命令，并将这些命令转换为 XMLA 消息，以用于 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例。 AMO 将 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例对象作为类提供给最终用户应用程序，具有运行命令的方法成员和保持 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 对象的数据的属性成员。  
  
 下图显示了 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 组件体系结构，包括了在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例中运行的所有主要元素和与该示例进行交互的所有用户组件。 该图还表明了访问该实例的唯一方法是通过 HTTP 或 TCP 使用 XML for Analysis (XMLA) 侦听器。  
  
 ![Analysis Services 系统体系结构关系图](../../../analysis-services/data-mining/media/analysisservicessystemarchitecture.gif "Analysis Services 系统体系结构关系图")  
  
## <a name="xmla-listener"></a>XMLA 侦听器  
 XMLA 侦听器组件处理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 与其客户端之间的所有 XMLA 通信。 可以使用 msmdsrv.ini 文件中的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] **端口** 配置设置来指定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例所侦听的端口。 此文件中的值 0 指示 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 侦听默认端口。 除非另有指定，否则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用下列默认的 TCP 端口：  
  
|端口|Description|  
|----------|-----------------|  
|2383|默认的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。|  
|2382|其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例的重定向程序。|  
|在服务器启动时动态分配|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]的命名实例。|  
  
 请参阅[Configure Windows Firewall to Allow Analysis Services Access](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)有关详细信息。  
  
## <a name="see-also"></a>另请参阅  
 [命名规则的对象&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/olap-physical/object-naming-rules-analysis-services.md)   
 [物理体系结构&#40;Analysis Services-多维数据&#41;](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)   
 [逻辑体系结构&#40;Analysis Services-多维数据&#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)  
  
  
