---
title: 从分析数据源中检索数据 |Microsoft Docs
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
- data retrieval [ADOMD.NET]
- retrieving data
- ADOMD.NET, data retrieval
- data retrieval [ADOMD.NET], about retrieving data
ms.assetid: 88358189-28aa-4bc7-8dda-5a92e3a012b8
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4e5595bd4e001b006cb1dfe62cba40cee3bbb30c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196417"
---
# <a name="retrieving-data-from-an-analytical-data-source"></a>从分析数据源检索数据
  在建立连接并创建查询后，您可以检索任何数据。 在 ADOMD.NET 中，可通过调用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象的 `Execute` 方法之一来使用三个不同的对象（<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>、<xref:System.Xml.XmlReader> 和 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>）进行数据检索。  
  
 这三个对象中的每个对象都可平衡交互功能和开销：  
  
-   *交互性*是指易用性和可用于通过对象模型的信息的量。  
  
-   *开销*指的对象模型生成通过网络连接到服务器对象模型中，并与对象模型检索数据的速度所需的内存量的流量。  
  
 为帮助您选择最适合您应用程序所需的数据检索对象，下表突出显示了每个对象的交互功能与开销之间的差异。  
  
|Object|交互|开销|保留维数|用法信息|  
|------------|-------------------|--------------|----------------------------|-----------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|最高|比较高，这会导致最慢的数据检索速度|是|[使用 CellSet 检索数据](retrieving-data-using-the-cellset.md)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>|中等|中等|“否”|[填充数据集从 DataAdapter](http://go.microsoft.com/fwlink/?LinkId=70016)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|中等|中等|“否”|[使用 AdomdDataReader 检索数据](retrieving-data-using-the-adomddatareader.md)|  
|<xref:System.Xml.XmlReader>|最低|最低，这会导致最快的数据检索速度|是|[使用 XmlReader 检索数据](retrieving-data-using-the-xmlreader.md)|  
  
## <a name="see-also"></a>请参阅  
 [ADOMD.NET 客户端编程](adomd-net-client-programming.md)  
  
  
