---
title: 用于分析的客户端体系结构要求服务开发 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- local mining models [Analysis Services]
- Analysis Services, architecture
- providers [Analysis Services]
- data pumps [Analysis Services]
- client architecture [Analysis Services]
- local cubes [Analysis Services]
ms.assetid: 03a8eb6b-159f-4a0a-afbe-06a2424b6090
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4eccbc79f0343403667b3aca7dbc159f59f7046b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37308467"
---
# <a name="client-architecture-requirements-for-analysis-services-development"></a>Analysis Services 开发的客户端体系结构要求
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支持瘦客户端体系结构。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]计算引擎是完全基于服务器的因此所有查询将在服务器上都解析。 因此，每个查询只需在客户端和服务器之间进行一次来回行程，从而使得性能可以随着查询复杂性的增加而伸缩。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的本机协议为 XML for Analysis (XML/A)。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 为客户端应用程序提供了数个数据访问接口，但是所有这些组件都使用 XML for Analysis 与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例进行通信。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 提供了数个不同的访问接口，以支持不同的编程语言。 访问接口借助 Internet 信息服务 (IIS)，并通过 TCP/IP 或 HTTP 发送和接收 SOAP 数据包中的 XML for Analysis 来与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器进行通信。 HTTP 连接使用由 IIS 实例化的 COM 对象（称为数据抽取），该对象充当 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据的管道。 数据抽取既不会以任何方式检查包含在 HTTP 流中的基础数据，也不会检查可用于数据库本身中任何代码的任何基础数据结构。  
  
 ![Analysis Services 的逻辑客户端体系结构](../../../analysis-services/dev-guide/media/as-clientarch9.gif "Analysis Services 的逻辑客户端体系结构")  
  
 Win32 客户端应用程序可使用 OLE DB for OLAP 接口或用于组件对象模型 (COM) 自动化语言（如 Microsoft Visual Basic®）的 Microsoft® ActiveX® 数据对象 (ADO) 对象模型连接到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器。 以 .NET 语言编码的应用程序可以使用 ADOMD.NET 连接到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器。  
  
 现有的应用程序只需使用一个 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 访问接口便可在不进行修改的情况下与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 进行通信。  
  
|编程语言|数据访问接口|  
|--------------------------|---------------------------|  
|C++|OLE DB for OLAP|  
|Visual Basic 6|ADO MD|  
|.NET 语言|ADO MD.NET|  
|支持 SOAP 的任何语言|XML for Analysis|  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的 Web 体系结构具有完全可伸缩的中间层，可方便小型和大型组织进行部署。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 为 Web 服务提供了广泛的中间层支持。 由 OLE DB for OLAP 和 ADO MD 支持 ASP 应用程序，ADOMD.NET 支持 ASP.NET 应用程序。 中间层（如下图中所示）可进行伸缩以供众多并发用户使用。  
  
 ![中间层体系结构的逻辑关系图](../../../analysis-services/dev-guide/media/as-midtierarch9.gif "中间层体系结构的逻辑关系图")  
  
 客户端应用程序和中间层应用程序都可以不通过访问接口而直接与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 进行通信。 客户端应用程序和中间层应用程序可以通过 TCP/IP、HTTP 或 HTTPS 使用 SOAP 数据包发送 XML for Analysis。 客户端可以使用任何支持 SOAP 的语言进行编码。 在这种情况下，尽管也可对使用 TCP/IP 与服务器建立的直接连接进行编码，但通信可由 Internet Information Services (IIS) 使用 HTTP 以最轻松的方式进行管理。 这是最不可能实现的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 客户端解决方案。  
  
## <a name="analysis-services-in-tabular-or-sharepoint-mode"></a>表格或 SharePoint 模式下的 Analysis Services  
 在中[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，可在 xVelocity 内存中分析引擎 (VertiPaq) 模式下的表格数据库和用于启动服务器[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]已发布到 SharePoint 站点的工作簿。  
  
 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 是支持创建和查询分别使用 SharePoint 或表格模式的内存中数据库的唯一客户端环境。 通过使用 Excel 创建嵌入的 PowerPivot 数据库和[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]工具包含在 Excel 工作簿中，作为 Excel.xlsx 文件的一部分保存。  
  
 但是，如果您将多维数据集数据导入到某一 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿中，则该工作簿可以使用在传统多维数据集中存储的数据。 如果其他 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿已发布到某一 SharePoint 站点，您还可以从该工作簿中导入数据。  
  
> [!NOTE]  
>  当您使用某一多维数据集作为 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿的数据源时，您从该多维数据集获取的数据将定义为 MDX 查询；但是，该数据将作为平展的快照导入。 您不能以交互方式使用数据或刷新来自多维数据集的数据。  
  
### <a name="interfaces-for-powerpivot-client"></a>PowerPivot 客户端的接口  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 通过使用针对 Analysis Services 的既定的接口和语言与工作簿内的 xVelocity 内存中分析引擎 (VertiPaq) 存储引擎交互： AMO 和 ADOMD.NET 以及 MDX 和 XMLA。 在该外接程序内，通过使用与 Excel、数据分析表达式 (DAX) 类似的公式语言定义度量值。 DAX 表达式嵌入在发送到进程内服务器的 XMLA 消息内。  
  
### <a name="providers"></a>访问接口  
 之间的通信[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]和 Excel 使用 MSOLAP OLEDB 访问接口 （11.0 版）。 在 MSOLAP 访问接口内，有四个可用于在客户端和服务器之间发送消息的不同的模块或传输。  
  
 **TCP/IP**正常客户端-服务器连接时使用。  
  
 **HTTP**用于通过 SSAS 数据抽取服务，或通过调用 SharePoint PowerPivot Web 服务 (WS) 组件的 HTTP 连接。  
  
 **INPROC**用于进程内引擎的连接。  
  
 **通道**保留与 SharePoint 场中 PowerPivot 系统服务进行通信。  
  
## <a name="see-also"></a>请参阅  
 [OLAP 引擎服务器组件](olap-engine-server-components.md)  
  
  
