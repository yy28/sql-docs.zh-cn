---
title: "ADOMD.NET 客户端功能 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: 0f5e16a1-dc2d-4c87-8551-985921bf069b
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 0a1047fbccf3e9437c3160891f502f9e2838c34a
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

---
# <a name="adomdnet-client-functionality"></a>ADOMD.NET 客户端功能
  与其他 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 数据访问接口一样，ADOMD.NET 也用作应用程序与数据源之间的桥梁。 但 ADOMD.NET 与其他 .NET Framework 数据访问接口的不同之处在于 ADOMD.NET 处理的是分析数据。 为了处理分析数据，ADOMD.NET 支持的功能与其他 .NET Framework 数据访问接口所支持的功能差异很大。 ADOMD.NET 不仅可检索数据，还可检索元数据并更改分析数据存储区的结构：  
  
 **检索元数据**  
 应用程序可使用架构行集或对象模型，进一步了解通过元数据检索从数据源检索的数据。 如可用的关键绩效指标 (KPI) 的类型、多维数据集中的维度和挖掘模型所需的参数等信息都可以发现。 元数据是对最重要*动态*需要用户输入，以确定类型、 深度和作用域的数据要检索的应用程序。 此类应用程序的例子有查询分析器、Microsoft Excel 以及其他查询工具。 元数据不太重要到*静态*执行一组预定义的操作的应用程序。  
  
 有关详细信息：[分析数据源中检索元数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)。  
  
 **检索数据**  
 数据检索是对存储在数据源中的信息的实际检索。 数据检索在知晓数据源结构的“静态”应用程序中是主要功能。 数据检索也是“动态”应用程序的最终结果。 一天中给定时间的 KPI 值、每个商店上一小时内的的自行车销售量以及影响雇员的年度业绩的因素，这些数据都是可以检索的。 检索数据对于任何查询应用程序都是至关重要的。  
  
 有关详细信息：[从分析的数据源检索数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)。  
  
 **更改分析数据的结构**  
 ADOMD.NET 还可用于实际更改分析数据存储区的结构。 虽然这通常是通过分析管理对象 (AMO) 对象模型进行的，但您也可以使用 ADOMD.NET 来发送 Analysis Services 脚本语言 (ASSL) 命令，从而创建、更改或删除服务器中的对象。  
  
 有关详细信息：[执行命令对分析数据源](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)，[使用分析管理对象 &#40; 进行开发AMO &#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)， [analysis Services 脚本语言 &#40;ASSL 为 XMLA &#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)  
  
 检索元数据、检索数据和更改数据结构均发生在典型 ADOMD.NET 应用程序的工作流中的特定点。  
  
## <a name="typical-process-flow"></a>典型处理流程  
 传统的 ADOMD.NET 应用程序在处理分析数据时，通常遵循相同的工作流：  
  
1.  首先，使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象与数据库建立连接。 打开连接时，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象会公开所连接到的服务器的元数据。 在动态应用程序中，其中的某些信息通常会显示给用户，以便用户做出选择，如查询哪个多维数据集。 应用程序可多次重用此步中创建的连接，以降低开销。  
  
     有关详细信息： [Establishing Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)  
  
2.  连接建立后，动态应用程序即可从服务器查询更多特定元数据。 对于静态应用程序，由于程序员事先知道应用程序要查询哪些对象，因此不需要检索这些元数据。 应用程序和用户可以在下一步骤中使用检索到的元数据。  
  
     有关详细信息：[分析数据源中检索元数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
3.  接下来，应用程序对服务器运行一条命令。 执行这一命令的目的既可以是检索其他元数据或检索数据，也可以是修改数据库结构。 对于这些任务中的任何一个，应用程序都可以使用先前确定的查询，也可以使用新检索的元数据创建其他查询。  
  
     有关详细信息：[分析数据源中检索元数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)，[从分析的数据源检索数据](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)，[执行命令对分析数据源](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)  
  
4.  命令发送到服务器后，服务器即开始向客户端返回元数据或数据。 可通过查看此信息<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>对象，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>对象，或**System.XmlReader**对象。  
  
 为了说明这种传统工作流，下面的示例包含了一个方法，该方法先打开一个与数据库的连接，再对一个已知多维数据集执行一条命令，然后检索结果并将其放入一个单元集。 随后，该单元集返回一个以制表符分隔的包含列标题、行标题和单元数据的字符串。  
  
 [!code-cs[Adomd.NetClient#ReturnCommandUsingCellSet](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/adomd-net-client-functio_1.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [ADOMD.NET 客户端编程](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  

