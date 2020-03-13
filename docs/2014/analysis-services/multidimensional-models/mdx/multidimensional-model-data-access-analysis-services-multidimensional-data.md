---
title: 多维模型数据访问（Analysis Services 多维数据） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, data access interfaces
- objects [Analysis Services], data access interfaces
- Analysis Services data access interfaces
- data retrieval [Analysis Services]
- retrieving data
- metadata [Analysis Services]
- data access interfaces [Analysis Services]
- manipulating objects [Analysis Services]
- Analysis Services data access interfaces, about data access interfaces
ms.assetid: 46388efb-3c78-47a2-b5c9-5a69ff394d03
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d6bea885a03d09da28d5f49ada36cf17375a507
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79217151"
---
# <a name="multidimensional-model-data-access-analysis-services---multidimensional-data"></a>多维模型数据访问（Analysis Services - 多维数据）
  使用本主题中的信息可以了解如何使用编程方法、脚本或客户端应用程序（内置用于连接您网络上的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器的支持）来访问 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 多维数据。  
  
 本主题包含以下各节：  
  
 [客户端应用程序](#bkmk_clientapps)  
  
 [查询语言](#bkmk_querylang)  
  
 [编程接口](#bkmk_api)  
  
##  <a name="bkmk_clientapps"></a>客户端应用程序  
 尽管 Analysis Services 提供可供您以编程方式构建或集成多维数据库的接口，但更常用的方法是使用对 Analysis Services 数据提供内置访问支持的 Microsoft 和其他软件供应商现有的客户端应用程序。  
  
 以下 Microsoft 应用程序支持本机连接到多维数据。  
  
### <a name="excel"></a>Excel  
 Analysis Services 多维数据经常使用数据透视表和数据透视图表控件呈现在 Excel 工作薄中。 数据透视表适用于多维数据，因为模型中的层次结构、聚合和导航构造与数据透视表的数据汇总功能十分吻合。 Excel 安装中包括 Analysis Services OLE DB 数据访问接口，便于更轻松地建立数据连接。 有关详细信息，请参阅 [连接到 SQL Server Analysis Services 或从其中导入数据](https://go.microsoft.com/fwlink/?linkID=215150)。  
  
### <a name="reporting-services-reports"></a>Reporting Services 报表  
 您可以使用报表生成器或报表设计器来创建使用 Analysis Services 数据库（其中包含分析数据）的报表。 报表生成器或报表设计器中都提供了 MDX 查询设计器，该设计器可用于键入或设计 MDX 语句，从可用数据源中检索数据。 有关详细信息，请参阅 [Reporting Services 支持的数据源 (SSRS)](../../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md) 和[针对 MDX 的 Analysis Services 连接类型 (SSRS)](../../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)。  
  
### <a name="performancepoint-dashboards"></a>PerformancePoint 面板  
 PerformancePoint 面板用于在 SharePoint 中创建记分卡，将业务表现与预定义度量值进行比照。 PerformancePoint 支持与 Analysis Services 多维数据建立数据连接。 有关详细信息，请参阅 [创建 Analysis Services 数据连接 (PerformancePoint Services)](https://go.microsoft.com/fwlink/?linkid=232471)。  
  
### <a name="sql-server-data-tools"></a>SQL Server Data Tools  
 模型设计器和报表设计器使用 SQL Server Data Tools 生成包括多维模型的解决方案。 在 Analysis Services 实例中部署该解决方案意味着创建您随后要从 Excel、Reporting Services 和其他商业智能客户端应用程序建立连接的数据库。  
  
 SQL Server Data Tools 基于 Visual Studio shell 构建，并使用项目来组织和包含模型。 有关详细信息，请参阅[使用 SQL Server Data Tools 创建多维模型 (SSDT)](../creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)。  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 对于数据库管理员，SQL Server Management Studio 是一个用于管理 SQL Server 实例（包括 Analysis Services 实例和多维数据库实例）的集成环境。 有关详细信息，请参阅 [SQL Server Management Studio](../../../ssms/sql-server-management-studio-ssms.md) 和 [连接到 Analysis Services](../../instances/connect-to-analysis-services.md)。  
  
##  <a name="bkmk_querylang"></a>查询语言  
 MDX 是用于从 OLAP 数据库中检索数据的行业标准查询和计算语言。 在 Analysis Services 中，MDX 是用于检索数据的查询语言，但也支持数据定义和数据操作。 MDX 编辑器内置在 SQL Server Management Studio、Reporting Services 和 SQL Server Data Tools 中。 您可以使用 MDX 编辑器创建即席查询或可重复使用的脚本（如果数据操作可重复）。  
  
 一些工具和应用程序（如 Excel）在内部使用 MDX 构造查询 Analysis Services 数据源。 您还可以通过将 MDX 语句放入 XMLA Execute 请求，以编程方式使用 MDX。  
  
 以下链接提供有关 MDX 的详细信息：  
  
 [使用 MDX 查询多维数据](querying-multidimensional-data-with-mdx.md)  
  
 [MDX &#40;Analysis Services 中的关键概念&#41;](../key-concepts-in-mdx-analysis-services.md)  
  
 [MDX 查询基础知识 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
 [MDX 脚本编写基础 &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)  
  
##  <a name="bkmk_api"></a>编程接口  
 如果要创建使用多维数据的自定义应用程序，访问数据所用的方法很可能属于以下类别之一：  
  
-   **XMLA**。 当您需要兼容多种操作系统和协议时，请使用 XMLA。 XMLA 提供了最大的灵活性，但往往会牺牲性能，同时增加编程的难度。  
  
-   **客户端库**。 当您要通过在 Microsoft Windows 操作系统上运行的客户端应用程序以编程方式访问数据时，请使用 Analysis Services 客户端库，如 ADOMD.NET、AMO 和 OLE DB。 客户端库使用对象模型和可提高性能的优化功能封装 XMLA。  
  
     ADOMD.NET 和 AMO 客户端库面向用托管代码编写的应用程序。 如果您的应用程序用本机代码编写，请使用 OLE DB for Analysis Services。  
  
 下表提供关于将 Analysis Services 连接到自定义应用程序所用的客户端库的更多详细信息和链接。  
  
|接口|说明|  
|---------------|-----------------|  
|Analysis Services 管理对象 (AMO)|AMO 是在代码中管理 Analysis Services 实例和多维数据库的主要对象模型。 例如，SQL Server Management Studio 使用 AMO 支持服务器和数据库管理。 有关详细信息，请参阅[使用分析管理对象 (AMO) 进行开发](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)。|  
|ADOMD.NET|ADOMD.NET 是在自定义应用程序中创建和访问多维数据的主要对象模型。 可以在托管客户端应用程序中使用 ADOMD.NET，以便使用通用 Microsoft .NET Framework 数据访问接口来检索 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 信息。 有关详细信息，请参阅 [使用 ADOMD.NET 进行开发](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net) 和 [ADOMD.NET 客户端编程](https://docs.microsoft.com/analysis-services/adomd/multidimensional-models-adomd-net-client/adomd-net-client-programming)。|  
|Analysis Services OLE DB 访问接口 (MSOLAP.dll)|您可以使用本机 OLE DB 访问接口以编程方式从非托管 API 访问 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 有关详细信息，请参阅 [Analysis Services OLE DB 提供程序访问接口（Analysis Services - 多维数据）](../../dev-guide/analysis-services-ole-db-provider-analysis-services-multidimensional-data.md)。|  
|架构行集|架构行集表是一种数据结构，其中包含关于在服务器上部署的多维模型的描述性信息，以及关于服务器上当前活动的信息。 作为编程人员，您可以通过在客户端应用程序中查询架构行集表，来检查存储在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上的元数据并且可以从该实例中检索支持和监视信息。 可以对以下编程接口使用架构行集：OLE DB、OLE DB for Analysis Services、OLE DB for Data Mining 或 XMLA。 有关详细信息，请参阅 [Analysis Services 架构行集](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets)。<br /><br /> 下面的列表说明了使用架构行集的几种方法：<br /><br /> 在 SQL Server Management Studio 或自定义报表中运行 DMV 查询，使用 SQL 语法访问架构行集。 有关详细信息，请参阅[使用动态管理视图 (DMV) 监视 Analysis Services](../../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)。<br /><br /> 编写可调用架构行集的 ADOMD.NET 代码。<br /><br /> 直接对 `Discover` 实例运行 XMLA [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 方法以检索架构行集信息。 有关详细信息，请参阅 [Discover 方法 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)。|  
|XMLA|XMLA 是可供 Analysis Services 编程人员使用的最低级别的 API，而且是所有 Analysis Services 数据访问方法中最基本的通用访问方法。 XMLA 是业界标准的基于 SOAP 的 XML 协议，它支持通过 HTTP 连接对所有标准多维数据源进行通用数据访问。 它使用 SOAP 来表示针对多维数据的请求和响应。 如果您的应用程序运行在 Windows 之外的平台上，则可以使用 XMLA 访问运行在网络中的 Windows 服务器上的多维数据库。 有关详细信息，请参阅 [在 Analysis Services 中使用 XMLA 开发](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)。|  
|Analysis Services 脚本语言 (ASSL)|ASSL 是一个适用于 XMLA 协议的 Analysis Services 扩展的描述性术语。 ASSL 扩展支持 Analysis Services 在 XMLA 协议基本设置之外使用 XMLA 构造，添加了数据定义、数据操作和数据控制支持。  XMLA 协议描述了 Execute 和 Discover 方法，ASSL 在此之外还添加了以下功能：<br /><br /> XMLA 脚本<br /><br /> XMLA 对象定义<br /><br /> XMLA 命令<br /><br /> <br /><br /> 有关详细信息，请参阅[使用 Analysis Services 脚本语言 (ASSL) 开发](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [连接到 Analysis Services](../../instances/connect-to-analysis-services.md)   
 [Analysis Services 脚本语言开发 &#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [在 Analysis Services 中通过 XMLA 进行开发](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [表格模型数据访问](../../tabular-models/tabular-model-data-access.md)  
  
  
