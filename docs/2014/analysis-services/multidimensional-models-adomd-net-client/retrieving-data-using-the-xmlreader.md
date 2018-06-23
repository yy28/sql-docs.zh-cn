---
title: 检索数据使用 XmlReader |Microsoft 文档
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
- retrieving data
- XmlReader object
- data retrieval [ADOMD.NET], XmlReader object
ms.assetid: 420ec40e-be2d-413a-b4b2-6d2b1756e270
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 257777c40c829921680b8fce333bd6e44f6f57fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024448"
---
# <a name="retrieving-data-using-the-xmlreader"></a>使用 XmlReader 检索数据
  `XmlReader` 类是 Microsoft .NET Framework 类库的 `System.Xml` 命名空间的一部分。由于 `XmlReader` 类还提供对数据的快速、非缓存、只进访问，因而与 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 类相似。 如果不需要使用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象获取数据的内存中分析视图，则 `XmlReader` 对象将是检索 XML 数据工具（尤其是大量数据）的最佳选择。 由于 `XmlReader` 用于传入数据，所以 `XmlReader` 在向调用方公开数据之前无需检索并缓存所有数据，如果使用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象将 XML for Analysis 响应转换为分析对象模型表示形式，则需要检索并缓存数据。  
  
 调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 方法时，`XmlReader` 类提供对 ADOMD.NET 接收的 XML for Analysis 响应的直接访问。 由于接收到的数据为原始 XML 数据，所以必须手动分析这些数据和元数据。 检索数据结束后，应关闭 `XmlReader` 对象。  
  
## <a name="retrieving-data-and-metadata"></a>检索数据和元数据  
 若要使用 `XmlReader` 类检索数据，请按下列步骤操作：  
  
1.  **创建对象的新实例。**  
  
     若要创建 `XmlReader` 类的新实例，请调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 方法。  
  
2.  **检索数据。**  
  
     在命令运行查询并返回 `XmlReader` 后，必须分析数据和元数据。 XML 数据和元数据由 XML for Analysis 访问接口所使用的本机格式表示。 对于大多数 XML for Analysis 访问接口，本机格式为 `MDDataSet` 格式。 `MDDataSet` 格式以正确的格式提供单元集的数据和元数据。 有关 `MDDataSet` 格式的详细信息，请参阅 XML for Analysis 规范。  
  
3.  **关闭读取器。**  
  
     使用完 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> 对象后，应始终调用 `XmlReader` 方法。 打开 `XmlReader` 后，`XmlReader` 将独占使用用于运行命令的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象。 您将无法使用该 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 运行任何命令，包括创建另一个 `XmlReader` 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>，直到您关闭原始的 `XmlReader` 为止。  
  
### <a name="example-of-retrieving-data-from-the-xmlreader"></a>从 XmlReader 检索数据的示例  
 下面的示例运行一条命令，并将数据检索为 `XmlReader`，以向控制台输出文件内容。  
  
 [!code-csharp[Adomd.NetClient#OutputDataWithXML](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#outputdatawithxml)]  
  
## <a name="see-also"></a>请参阅  
 [从分析数据源检索数据](retrieving-data-from-an-analytical-data-source.md)   
 [使用单元集中检索数据](retrieving-data-using-the-cellset.md)   
 [使用 AdomdDataReader 检索数据](retrieving-data-using-the-adomddatareader.md)  
  
  