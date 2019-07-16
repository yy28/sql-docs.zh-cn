---
title: 逻辑体系结构 (Analysis Services-多维数据) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b6b33ffbf59cf05bc5455d3daac437e9e79407c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165604"
---
# <a name="understanding-microsoft-olap-logical-architecture"></a>了解 Microsoft OLAP 逻辑体系结构
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用服务器和客户端组件提供联机分析处理 (OLAP) 和商业智能应用程序的数据挖掘功能：  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的服务器组件是作为 Microsoft Windows 服务来实现。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 与每个实例在同一计算机上支持多个实例[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]作为 Windows 服务的单独实例实现。  
  
-   客户端使用公用标准 XML for Analysis (XMLA) 与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 进行通信，作为一项 Web 服务，XMLA 是基于 SOAP 的协议，用于发出命令和接收响应。 还可以通过 XMLA 提供客户端对象模型，可以使用托管提供程序（例如，ADOMD.NET）或本机 OLE DB 访问接口来访问该模型。  
  
-   可以使用以下语言发出查询命令：SQL;多维表达式 (MDX)，一种行业标准查询语言以进行分析;或数据挖掘扩展插件 (DMX) 面向数据挖掘的行业标准查询语言。 Analysis Services 脚本语言 (ASSL) 还可以用来管理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库对象。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 还支持本地多维数据集引擎，已断开连接的客户端上的应用程序可在该引擎的帮助下，在本地浏览已存储的多维数据。 有关详细信息，请参阅[Analysis Services 开发的客户端体系结构要求](../../../analysis-services/multidimensional-models/olap-physical/client-architecture-requirements-for-analysis-services-development.md)  
  
## <a name="in-this-section"></a>本节内容  
 **逻辑体系结构概述**  
 [逻辑体系结构概述&#40;Analysis Services-多维数据&#41;](../../../analysis-services/multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md)  
  
 **服务器对象**  
 [服务器对象&#40;Analysis Services-多维数据&#41;](../../../analysis-services/multidimensional-models/olap-logical/server-objects-analysis-services-multidimensional-data.md)  
  
 **数据库对象**  
 [数据库对象（Analysis Services - 多维数据）](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
 **维度对象**  
 [维度对象&#40;Analysis Services-多维数据&#41;](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-objects-analysis-services-multidimensional-data.md)  
  
 **多维数据集对象**  
 [多维数据集对象&#40;Analysis Services-多维数据&#41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
 **代码访问安全性**  
 [用户访问的安全体系结构](http://msdn.microsoft.com/library/71b44e10-2bd0-44f7-8de9-7c8f5b7ac082)  
  
## <a name="see-also"></a>请参阅  
 [了解 Microsoft OLAP 体系结构](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)   
 [物理体系结构&#40;Analysis Services-多维数据&#41;](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)  
  
  
