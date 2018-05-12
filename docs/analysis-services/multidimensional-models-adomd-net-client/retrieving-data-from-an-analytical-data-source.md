---
title: 从分析数据源检索数据 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 50ded9ed90f9090d7a711c2d0cdb049e942896b8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="retrieving-data-from-an-analytical-data-source"></a>从分析数据源检索数据
  在建立连接并创建查询后，您可以检索任何数据。 In ADOMD.NET，您可以使用三个不同的对象数据 (<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>， <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>，和<xref:System.Xml.XmlReader>) 通过调用之一**执行**方法<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>对象。  
  
 这三个对象中的每个对象都可平衡交互功能和开销：  
  
-   *交互性*指的易用性和可用于通过对象模型的信息的量。  
  
-   *开销*引用的对象模型生成通过网络连接到服务器对象模型中，以及与该对象模型中检索数据的速度所需的内存量的流量。  
  
 为帮助您选择最适合您应用程序所需的数据检索对象，下表突出显示了每个对象的交互功能与开销之间的差异。  
  
|对象|交互|开销|保留维数|用法信息|  
|------------|-------------------|--------------|----------------------------|-----------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|最高|比较高，这会导致最慢的数据检索速度|是|[使用 CellSet 检索数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>|中等|中等|否|[填充数据集从 DataAdapter](http://go.microsoft.com/fwlink/?LinkId=70016)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|中等|中等|否|[使用 AdomdDataReader 检索数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)|  
|<xref:System.Xml.XmlReader>|最低|最低，这会导致最快的数据检索速度|是|[使用 XmlReader 中检索数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ADOMD.NET 客户端编程](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
