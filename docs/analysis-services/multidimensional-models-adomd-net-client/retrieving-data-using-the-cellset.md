---
title: 检索使用单元集的数据 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9954141f2f4c69d42be879960ea183fc11d4e162
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="retrieving-data-using-the-cellset"></a>使用 CellSet 检索数据
  在检索分析数据时，<xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象提供了最大的交互功能和灵活性。 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象是分层数据和元数据的内存缓存，用于保留数据的原始维数。 还可以在连接或断开连接状态中对 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象进行遍历。 由于此断开连接的功能，<xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象还可用于以任何顺序查看数据和元数据，并为数据检索提供最全面的对象模型。 此断开连接的功能还会导致 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象有最大的开销，并成为要填充的最慢的 ADOMD.NET 数据检索对象模型。  
  
## <a name="retrieving-data-in-a-connected-state"></a>在连接状态下检索数据  
 若要使用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象检索数据，请按以下步骤操作：  
  
1.  **创建对象的新实例。**  
  
     若要创建 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象的新实例，请调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A> 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 方法。  
  
2.  **标识元数据。**  
  
     除了检索数据，ADOMD.NET 还将检索单元集的元数据。 在该命令运行查询并返回 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 后，即可通过各种对象检索元数据。 客户端应用程序需要使用此元数据显示单元集数据并与之交互。 例如，许多客户端应用程序提供对单元集中的特定位置进行细分，或分层显示特定位置的子位置的功能。  
  
     在 ADOMD.NET 中，<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Axes%2A> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.FilterAxis%2A> 和 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 属性分别代表所返回单元集中的查询轴和切片器轴的元数据。 这两个属性都返回对 <xref:Microsoft.AnalysisServices.AdomdClient.Axis> 对象的引用，这些引用又包含每个轴上表示的位置。  
  
     每个 <xref:Microsoft.AnalysisServices.AdomdClient.Axis> 对象包含 <xref:Microsoft.AnalysisServices.AdomdClient.Position> 对象的集合，这些对象表示可用于该轴的元组集。 每个 <xref:Microsoft.AnalysisServices.AdomdClient.Position> 对象表示一个包含一个或多个成员的元组，这些成员由 <xref:Microsoft.AnalysisServices.AdomdClient.Member> 对象的集合表示。  
  
3.  **从单元集集合中检索数据。**  
  
     除了检索元数据，ADOMD.NET 还将检索单元集的数据。 在该命令运行了查询并返回 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 后，即可使用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A> 的 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 集合检索数据。 此集合包含为查询中的所有轴的交点计算出的值。 因此，有多个可用于访问每个交点或单元的索引器。 有关索引器的列表，请参阅 <xref:Microsoft.AnalysisServices.AdomdClient.CellCollection.Item%2A>。  
  
### <a name="example-of-retrieving-data-in-a-connected-state"></a>在连接状态下检索数据的示例  
 下面的示例连接到本地服务器，然后对该连接运行命令。 该示例通过使用分析结果**单元集**对象模型： 列的标题 （元数据） 均从第一个轴，检索，并且从第二个轴，检索到的每一行的标题 （元数据） 和交叉数据通过使用<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A>集合。  
  
 [!code-cs[Adomd.NetClient#ReturnCommandUsingCellSet](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_0_1.cs)]  
  
## <a name="retrieving-data-in-a-disconnected-state"></a>在断开连接状态下检索数据  
 通过加载从前一查询返回的 XML，可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象提供全面的方法来浏览分析数据，而不需要活动连接。  
  
> [!NOTE]  
>  不是 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象中提供的对象的所有属性在断开连接的状态下都可用。 有关详细信息，请参阅<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A>。  
  
### <a name="example-of-retrieving-data-in-a-disconnected-state"></a>在断开连接状态下检索数据的示例  
 下面的示例与本主题中前面介绍的元数据和数据示例类似。 但是，在下面的示例命令开始运行，通过调用<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>，并且结果返回为**System.Xml.XmlReader**。 该示例然后填充<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>使用此对象**System.Xml.XmlReader**与<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A>方法。 虽然此示例加载**System.Xml.XmlReader**立即，您可以在其中缓存到硬盘读取器包含或传输数据通过任何方式之前将数据加载到不同的应用程序复制到的 XML单元集。  
  
 [!code-cs[Adomd.NetClient#DemonstrateDisconnectedCellset](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_0_2.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [从分析数据源检索数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)   
 [使用 AdomdDataReader 检索数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)   
 [使用 XmlReader 中检索数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)  
  
  
