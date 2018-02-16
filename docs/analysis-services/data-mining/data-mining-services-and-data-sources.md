---
title: "数据挖掘服务和数据源 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b26fd6e3-7d87-4f66-ab47-5303b51b87da
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 78e67d346c451c258e806e6f888aef096e7d4256
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="data-mining-services-and-data-sources"></a>数据挖掘服务和数据源
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
数据挖掘需要连接到 SQL Server Analysis Services 实例才能工作。 数据挖掘不需要多维数据集中的数据，建议使用关系源；但是，数据挖掘使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 引擎提供的组件。  
  
 本主题提供了在连接到 SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例以创建、处理、部署或查询数据挖掘模型时需要了解的信息。  
  
## <a name="data-mining-services"></a>数据挖掘服务  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的服务器组件是应用程序 msmdsrv.exe，该程序通常作为一项 Windows 服务来运行。 该应用程序包含安全组件、一个 XML for Analysis (XMLA) 侦听器组件、一个查询处理器组件以及执行下列功能的多个其他内部组件：  
  
-   分析从客户端接收的语句  
  
-   管理元数据  
  
-   处理翻译  
  
-   处理计算  
  
-   存储维度和单元数据  
  
-   创建聚合  
  
-   计划查询  
  
-   缓存对象  
  
-   管理服务器资源  
  
### <a name="xmla-listener"></a>XMLA 侦听器  
 XMLA 侦听器组件处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 与其客户端之间的所有 XMLA 通信。 可以使用 msmdsrv.ini 文件中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] **端口** 配置设置来指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例所侦听的端口。 此文件中的值 0 指示 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 侦听默认端口。 除非另有指定，否则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用下列默认的 TCP 端口：  
  
|端口|Description|  
|----------|-----------------|  
|2383|默认的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例。|  
|2382|其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的重定向程序。|  
|在服务器启动时动态分配|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的命名实例。|  
  
 有关控制此服务所用端口的详细信息，请参阅 [将 Windows 防火墙配置为允许 Analysis Services 访问](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
## <a name="connecting-to-data-sources"></a>连接到数据源  
 每次创建或更新数据挖掘结构或模型时，都应使用由数据源定义的数据。 数据源不包含数据（可能包括 Excel 工作簿、文本文件和 SQL Server 数据库）；它只定义连接信息。  数据源视图 (DSV) 将充当数据源顶部的抽象层，并修改或映射从源中获得的数据。  
  
 介绍这些源各自的连接要求不在本主题讨论的范围内。 有关详细信息，请参阅访问接口的相关文档。 但一般来说，您在与访问接口进行交互时应了解 Analysis Services 的以下要求：  
  
-   因为数据挖掘是由服务器提供的服务，所以必须为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例提供对数据源的访问权限。  访问权限包含两个方面：位置和标识。  
  
     **位置** 意味着，如果使用仅存储在计算机上的数据生成一个模型，然后将该模型部署到服务器，则该模型会因找不到数据源而无法处理。 若要解决此问题，您可能需要将数据传入运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的同一 SQL Server 实例，或将文件移至共享位置。  
  
     **标识** 表示 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 上的服务必须能使用相应的凭据打开数据文件或数据源。 例如，在生成模型时，您可能已具有查看数据的不受限权限，而正在处理和更新服务器上的模型的用户可能具有对数据的受限访问权限或不具有对数据的访问权限，这会导致无法处理或影响模型内容。 用于连接到远程数据源的帐户必须至少具有对数据的读取权限。  
  
-   移动模型时，上述要求将适用：您必须设置对旧数据源的位置的适当访问权、复制数据源或配置新数据源。 此外，您必须传输登录名和角色，或设置权限以允许在新位置处理和更新数据挖掘对象。  
  
## <a name="configuring-permissions-and-server-properties"></a>配置权限和服务器属性  
 数据挖掘需要对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库具有其他权限。 可以使用[“Analysis Server 属性”对话框 (Analysis Services)](http://msdn.microsoft.com/library/b01ec658-c191-49c9-a6cb-549b21a368ab) 设置大多数数据挖掘属性。  
  
 有关可配置属性的详细信息，请参阅[ Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 下面的服务器属性与数据挖掘有特殊关系：  
  
-   **AllowAdHocOpenRowsetQueries** 控制对 OLE DB 访问接口的即席访问，该接口直接加载到服务器内存空间。  
  
    > [!IMPORTANT]  
    >  为了提高安全性，建议您将此属性设置为 **false**。 默认值是 **false**秒。 但是，即使此属性设置为 **false**，用户仍可以继续创建单独查询，并且可以对允许的数据源使用 OPENQUERY。  
  
-   **AllowedProvidersInOpenRowset** 指定启用即席访问时的访问接口。 通过输入一个以逗号分隔的 ProgID 列表，您可以指定多个访问接口。  
  
-   **MaxConcurrentPredictionQueries** 控制服务器上由预测引起的负载。 默认值 0 允许对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 执行不受限制的查询，对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard 最多执行五次并发查询。 超出限制的查询将被序列化，并且可能超时。  
  
 服务器还提供了控制可使用哪些数据挖掘算法（包括对算法的所有限制）以及所有数据挖掘服务的默认值的其他属性。 但是，没有任何设置可以专门控制对数据挖掘存储过程的访问。 有关详细信息，请参阅 [Data Mining Properties](../../analysis-services/server-properties/data-mining-properties.md)。  
  
 还可以设置允许用户优化服务器并控制客户端使用的安全性的属性。 有关详细信息，请参阅 [Feature Properties](../../analysis-services/server-properties/feature-properties.md)。  
  
> [!NOTE]  
>  有关在各个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中对插件算法的支持的详细信息，请参阅 [SQL Server 2012 各个版本支持的功能](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473)。  
  
## <a name="programmatic-access-to-data-mining-objects"></a>对数据挖掘对象的编程访问  
 您可以使用下列对象模型创建与 Analysis Services 数据库的连接和处理数据挖掘对象：  
  
 **ADO** 使用 OLE DB 连接到 Analysis Services 服务器。 使用 ADO 时，客户端仅限于架构行集查询和 DMX 语句。  
  
 **ADO.NET** 与其他访问接口相比，可以更好地与 SQL Server 访问接口进行交互。 使用数据适配器存储动态行集。 使用数据集对象，该数据集对象是作为数据表存储的服务器数据的缓存，可将该服务器数据更新或另存为 XML 格式。  
  
 **ADOMD.NET** 为处理数据挖掘和 OLAP 而优化的托管数据访问接口。 ADOMD.NET 速度比 ADO.NET 更快，并且更能有效地利用内存。 您还可以通过 ADOMD.NET 检索有关服务器对象的元数据。 建议用于客户端应用程序，除非 .NET 不可用。  
  
 **Server ADOMD** 用于在服务器上直接访问 Analysis Services 对象的对象模型。 供 Analysis Services 存储过程使用；不能用于客户端。  
  
 替换决策支持对象 (DSO) 的 Analysis Services 的**AMO** 管理接口。 与使用其他接口相比，在使用 AMO 时，循环访问对象等操作需要更高的权限。 这是因为 AMO 直接访问元数据，而 ADOMD.NET 和其他接口仅访问数据库架构。  
  
### <a name="browse-and-query-access-to-servers"></a>对服务器的浏览和查询访问权限  
 可通过在 OLAP/数据挖掘模式下使用 Analysis Service 实例来执行所有类型的预测，但具有下列限制：  
  
-   如果使用 Server ADOMD，则可以在不进行连接的情况下使用 DMX 访问该服务器。 然后可以将结果直接复制到数据表中。 但是，不能将 Server ADOMD 用于远程实例；您只能查询本地服务器。  
  
-   对于数据挖掘，ADO.NET 不支持命名参数。 您必须使用 ADOMD.NET。  
  
-   通过 ADOMD.NET，您可以传递整个表以将其作为参数使用；因此，您可以使用客户端上的数据或服务器无法使用的数据。 您还可以将具有形状的表作为预测输入使用。  
  
### <a name="using-data-mining-stored-procedures"></a>使用数据挖掘存储过程  
 存储过程的一个常见用途是封装查询以便重复使用。 客户端可以使用 CALL 来运行存储过程，包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 系统存储过程。  
  
 如果该过程返回数据集，客户端将接收具有嵌套表（包含行）的数据集或数据表。 例如，如果根据模型内容创建查询，查询将返回整个模型。 若要避免返回过多的行，您可以使用 ADOMD+ 对象模型编写存储过程。  
  
 若要编写服务器存储过程，则必须引用 Microsoft.AnalysisServices.AdomdServer 命名空间。 有关如何创建和使用存储过程的详细信息，请参阅 [User Defined Functions and Stored Procedures](../../analysis-services/multidimensional-models-adomd-net-server/user-defined-functions-and-stored-procedures.md)。  
  
> [!NOTE]  
>  存储过程不能用于更改数据服务器对象的安全性。 执行存储过程时，将使用用户的当前上下文来确定对所有服务器对象的访问权限。 因此，对于访问的任何数据库对象，用户必须拥有相应权限。  
  
## <a name="see-also"></a>另请参阅  
 [物理体系结构（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)   
 [物理体系结构 &#40;Analysis Services-数据挖掘 &#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [数据挖掘解决方案和对象的管理](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md)  
  
  
