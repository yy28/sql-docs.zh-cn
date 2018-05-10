---
title: ADOMD.NET 客户端编程 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ef37a558e3e8c0fb9b932cffe223508121b9103
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="adomdnet-client-programming"></a>ADOMD.NET 客户端编程
  ADOMD.NET 客户端组件驻留在**Microsoft.AnalysisServices.AdomdClient** （中 microsoft.analysisservices.adomdclient.dll) 命名空间。 这些客户端组件提供的功能的客户端和中间层应用程序轻松地查询数据和元数据来自分析数据存储区，如[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
## <a name="using-the-adomdnet-client-objects"></a>使用 ADOMD.NET 客户端对象  
 查询分析数据源时，有一组常见任务需要执行。 下表介绍了这些常见任务，您通常在这些任务中使用 ADOMD.NET 客户端对象执行此类查询。  
  
|任务|Description|  
|----------|-----------------|  
|[建立 Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)|在 ADOMD.NET 中，使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象建立与分析数据源（例如 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库）的连接。 可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象从分析数据源运行命令、检索数据和元数据。|  
|[从分析数据源检索元数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)|建立连接后，可以使用各种对象检索有关基础数据源的信息。 此功能允许应用程序适应它所连接到的数据源。|  
|[对分析数据源执行命令](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 对象提供针对基础分析数据源运行命令所必需的接口。|  
|[从分析数据源检索数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)|命令运行后，无法检索和分析使用数据<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>， <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>，或**System.XmlReader**对象。|  
|[In ADOMD.NET 执行事务](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-performing-transactions.md)|本表的前面几行中列出的所有操作都可以在已提交读事务中发生，在该事务中读取数据时保持共享锁以避免脏读。 但在事务结束之前仍可更改数据，从而产生不可重复的读取或虚拟数据。 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 对象在 ADOMD.NET 中提供事务功能。|  
  
 与 ADOMD.NET 对象层次结构的交互通常从最顶层的一个或多个对象开始（如下表所述）。  
  
|若要|使用此对象|  
|--------|---------------------|  
|连接到分析数据源|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象表示与数据源之间的连接以及数据源元数据。 例如，你可以连接到[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]本地多维数据集 (.cub) 文件，并检查<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Cubes%2A>属性来获取有关存在多维数据集在分析数据源上的元数据。 此对象还表示的实现**IDbConnection**接口，所需的所有.NET Framework 数据提供程序的接口。|  
|发现数据源的数据挖掘功能|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象公开若干挖掘集合：<br /><br /><br /><br /> <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection> 包含数据源中所有挖掘模型的列表。<br /><br /><br /><br /> <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection> 提供有关可用挖掘算法的信息。<br /><br /><br /><br /> <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection> 公开有关服务器上的挖掘结构的信息。|  
|查询数据源|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 对象表示将发送到服务器的语句或查询。 与数据源建立连接后，即可使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 对象以支持的语言运行语句，例如多维表达式 (MDX) 或数据挖掘扩展插件 (DMX)。 还可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 对象以 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 对象形式返回结果。|  
|以快速有效的方法检索数据|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader><br /> 可通过调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> 方法来创建 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>。 此对象实现**IDbDataReader**接口从**System.Data**的.NET Framework 类库的命名空间。|  
|检索带有最多元数据的分析数据|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet><br /> 可通过调用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A> 方法来创建 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>。 在 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 返回 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 后，即可检查 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 包含的分析数据。|  
|检索有关多维数据集的元数据，例如可用维度、度量值、命名集等|<xref:Microsoft.AnalysisServices.AdomdClient.CubeDef><br /> <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> 表示有关多维数据集的元数据。 从 <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> 引用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>。|  
|检索数据使用**System.Data.IDbDataAdapter**接口|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter> 提供对现有 .NET Framework 客户端应用程序的只读支持。|  
  
## <a name="see-also"></a>另请参阅  
 [ADOMD.NET Server 编程](../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)   
 [使用 ADOMD.NET 进行开发](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
  
