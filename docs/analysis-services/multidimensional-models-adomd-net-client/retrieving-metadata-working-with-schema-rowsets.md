---
title: "Working with Schema Rowsets in ADOMD.NET |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- metadata [ADOMD.NET]
- retrieving metadata
- schema rowsets [ADOMD.NET]
ms.assetid: 7bf75bf8-f1e1-44f6-ac42-c38a681654cf
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4045c7b677129bcc7b72b8ed46fa84aed95e49f5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="retrieving-metadata---working-with-schema-rowsets"></a>检索元数据-使用架构行集
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]当你需要比 ADOMD.NET 对象模型中可用的多个元数据时，ADOMD.NET 提供了有关 Analysis (XMLA)、 OLE DB、 OLE DB for OLAP 和 OLE DB for 数据挖掘架构行集检索完整范围的 XML 的功能：  
  
 **分析元数据的 XML**  
 XML for Analysis 架构行集可提供检索有关服务器的低级别信息的方法。 提供的信息包括服务器上可用的数据源、访问接口保留的关键字、访问接口支持的文字等。 您甚至可以使用 XML for Analysis 架构行集发现访问接口支持的所有架构行集。  
  
 有关详细信息： [XML for Analysis 架构行集](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 **OLE DB 元数据**  
 OLE DB 架构行集可提供从各种访问接口检索信息的行业标准方法。  
  
 有关详细信息： [OLE DB 架构行集合](../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
 **OLAP 元数据**  
 为分析数据源提供的架构信息包括可从分析数据源获取的数据库或目录、数据库中的多维数据集和挖掘模型、数据源中存在的多维数据集的角色等。  
  
 有关详细信息： [OLE DB for OLAP 架构行集](../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
 **数据挖掘元数据**  
 除了 OLAP 元数据之外，还可以使用架构行集检索数据挖掘元数据。 可用的行集可公开数据库中的可用数据挖掘模型、可用挖掘算法、算法所需的参数、挖掘结构等相关信息。  
  
 有关详细信息：[数据挖掘架构行集](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
 对于每个不同的架构行集，可使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 方法通过传递 GUID 或 XMLA 名称从行集检索元数据。  
  
## <a name="retrieving-metadata-by-passing-guids"></a>通过传递 GUID 检索元数据  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid> 类包含一个字段列表，这些字段表示访问接口和分析数据源最常支持的架构行集。 若要从访问接口或分析数据源检索常规和特定于访问接口的元数据，可通过下列方法之一使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid> 对象中包含的 GUID。  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
> [!NOTE]  
>  ADOMD.NET 数据访问接口可通过特定访问接口和分析数据源提供的功能公开架构信息。 每个访问接口和数据源都可能提供不同的元数据。  
  
## <a name="retrieving-metadata-by-passing-xmla-names"></a>通过传递 XMLA 名称检索元数据  
 以下方法将 XMLA 架构名称作为参数，该架构名称可标识要返回的架构信息，以及一组对这些返回列的限制：  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
 每个这些方法返回的实例**数据集**使用的架构信息填充的对象。 **数据集**对象是从**System.Data**的 Microsoft.NET Framework 类库的命名空间。  
  
## <a name="example"></a>示例  
 在下面的示例中，GetActions 函数采用连接、 多维数据集名称、 坐标和坐标类型，以检索[MDSCHEMA_ACTIONS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-actions-rowset.md)，并在所选的坐标时返回可用的操作。  
  
 [!code-cs[Adomd.NetClient#GetActions](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-metadata-work_0_1.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [从分析数据源检索元数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  
