---
title: ADOMD.NET 客户端编程 |Microsoft 文档
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
- programming [ADOMD.NET]
- ADOMD.NET, programming
ms.assetid: 55156115-ecd1-4ed9-876e-23406af9bbf9
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9faa64cce77c883ed6adb86bca6d50f32f015c97
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128868"
---
# <a name="adomdnet-client-programming"></a>ADOMD.NET 客户端编程
  ADOMD.NET 客户端组件位于 `Microsoft.AnalysisServices.AdomdClient` 命名空间 (microsoft.analysisservices.adomdclient.dll) 中。 这些客户端组件提供的功能的客户端和中间层应用程序轻松地查询数据和元数据来自分析数据存储区，如[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
## <a name="using-the-adomdnet-client-objects"></a>使用 ADOMD.NET 客户端对象  
 查询分析数据源时，有一组常见任务需要执行。 下表介绍了这些常见任务，您通常在这些任务中使用 ADOMD.NET 客户端对象执行此类查询。  
  
|任务|Description|  
|----------|-----------------|  
|[在 ADOMD.NET 中建立连接](connections-in-adomd-net.md)|在 ADOMD.NET 中，使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象建立与分析数据源（例如 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库）的连接。 可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象从分析数据源运行命令、检索数据和元数据。|  
|[从分析数据源检索元数据](retrieving-metadata-from-an-analytical-data-source.md)|建立连接后，可以使用各种对象检索有关基础数据源的信息。 此功能允许应用程序适应它所连接到的数据源。|  
|[对分析数据源执行命令](executing-commands-against-an-analytical-data-source.md)|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 对象提供针对基础分析数据源运行命令所必需的接口。|  
|[从分析数据源检索数据](retrieving-data-from-an-analytical-data-source.md)|运行命令后，可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>、<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 或 `System.XmlReader` 对象检索和分析数据。|  
|[在 ADOMD.NET 中执行事务](../../relational-databases/native-client-ole-db-transactions/transactions.md)|本表的前面几行中列出的所有操作都可以在已提交读事务中发生，在该事务中读取数据时保持共享锁以避免脏读。 但在事务结束之前仍可更改数据，从而产生不可重复的读取或虚拟数据。 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 对象在 ADOMD.NET 中提供事务功能。|  
  
 与 ADOMD.NET 对象层次结构的交互通常从最顶层的一个或多个对象开始（如下表所述）。  
  
|若要|使用此对象|  
|--------|---------------------|  
|连接到分析数据源|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象表示与数据源之间的连接以及数据源元数据。 例如，你可以连接到[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]本地多维数据集 (.cub) 文件，并检查<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Cubes%2A>属性来获取有关存在多维数据集在分析数据源上的元数据。 此对象还表示 `IDbConnection` 接口的实现，该接口是所有 .NET Framework 数据访问接口必需的。|  
|发现数据源的数据挖掘功能|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象公开若干挖掘集合：<br /><br /> -<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection>包含的数据源中的每个挖掘模型列表。<br />-<xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection>提供有关可用的挖掘算法的信息。<br />-<xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection>公开有关挖掘结构在服务器上的信息。|  
|查询数据源|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 对象表示将发送到服务器的语句或查询。 与数据源建立连接后，即可使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 对象以支持的语言运行语句，例如多维表达式 (MDX) 或数据挖掘扩展插件 (DMX)。 还可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 对象以 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 对象形式返回结果。|  
|以快速有效的方法检索数据|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader><br /> 可通过调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> 方法来创建 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>。 此对象实现 .NET Framework 类库的 `IDbDataReader` 命名空间的 `System.Data` 接口。|  
|检索带有最多元数据的分析数据|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet><br /> 可通过调用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A> 方法来创建 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>。 在 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 返回 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 后，即可检查 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 包含的分析数据。|  
|检索有关多维数据集的元数据，例如可用维度、度量值、命名集等|<xref:Microsoft.AnalysisServices.AdomdClient.CubeDef><br /> <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> 表示有关多维数据集的元数据。 从 <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> 引用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>。|  
|使用 `System.Data.IDbDataAdapter` 接口检索数据|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter> 提供对现有 .NET Framework 客户端应用程序的只读支持。|  
  
## <a name="see-also"></a>请参阅  
 [ADOMD.NET Server 编程](../multidimensional-models-adomd-net-server/adomd-net-server-programming.md)   
 [使用 ADOMD.NET 进行开发](../multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
  