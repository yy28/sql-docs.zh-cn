---
title: Reporting Services 中的数据连接、数据源和连接字符串 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], data sources
- reports [Reporting Services], data
- expressions [Reporting Services], data sources
- data sources [Reporting Services], connections
- connection strings [Reporting Services]
- shared data sources [Reporting Services]
- Reporting Services, data sources
- logins [Reporting Services]
ms.assetid: 4d8f0ae1-102b-4b3d-9155-fa584c962c9e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 88f843db8280220b75025dc286fe692957bf2b77
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78173916"
---
# <a name="data-connections-data-sources-and-connection-strings-in-reporting-services"></a>Data Connections, Data Sources, and Connection Strings in Reporting Services
  若要在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表中包含数据，必须首先创建“数据源” ** 和“数据集” **。 本主题解释数据源的类型、如何创建数据源以及与数据源凭据相关的重要信息。 数据源包含数据源类型、连接信息以及要使用的凭据的类型。 有两种类型的数据源：嵌入数据源和共享数据源。 嵌入数据源在报表中定义并只由该报表使用。 共享数据源独立于报表定义并可由多个报表使用。 有关详细信息，请参阅[嵌入和共享的数据连接或数据源（报表生成器和 SSRS）](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)和[嵌入数据集和共享数据集（报表生成器和 SSRS）](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)。

||
|-|
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 本机模式 &#124; [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式|

> [!NOTE]
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]



##  <a name="embedded-and-shared-data-sources"></a><a name="bkmk_data_sources"></a>嵌入数据源和共享数据源
 嵌入数据源和共享数据源的区别在于创建、存储和管理它们的方式不同。

-   在报表设计器中，将嵌入数据源或共享数据源作为 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 项目的一部分创建。 您可以控制是在本地使用它们以便进行预览，还是将其作为项目的一部分部署到报表服务器或 SharePoint 站点。 您可以使用已安装在您的计算机上和安装在报表服务器或 SharePoint 站点（在其中部署您的报表）上的自定义数据扩展插件。

     系统管理员可以安装和配置其他数据处理扩展插件和 .NET Framework 数据访问接口。 有关详细信息，请参阅[数据处理扩展插件和 .NET Framework 数据提供程序 (SSRS)](report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)。

     开发人员可以使用 <xref:Microsoft.ReportingServices.DataProcessing> API 创建数据处理扩展插件以支持其他类型的数据源。

-   在报表生成器中，浏览到某一报表服务器或 SharePoint 站点并选择共享数据源，或者在报表中创建嵌入数据源。 不能在报表生成器中创建共享数据源。 不能在报表生成器中使用自定义数据扩展插件

##  <a name="built-in-data-extensions"></a><a name="bkmk_DataConnections"></a>内置数据扩展插件
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的内置数据扩展插件包含以下类型的数据连接：

-   Microsoft SQL Server

-   Microsoft SQL Server Analysis Services

-   Microsoft SharePoint 列表

-   [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]

-   Microsoft SQL Server Parallel Data Warehouse

-   OLE DB

-   Oracle

-   SAP NetWeaver BI

-   Hyperion Essbase

-   Teradata

-   XML

-   ODBC

-   用于 Power View 的 Microsoft BI 语义模型：在配置用于 PowerPivot 库和 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]的 SharePoint 站点上，此数据源类型可用。 此数据源类型仅可用于 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 演示文稿。 有关详细信息，请参阅 [建立用于 Power View 的完美 BI 语义表格模型](https://technet.microsoft.com/video/building-the-perfect-bi-semantic-tabular-models-for-power-view.aspx)。

 有关 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持的数据源和版本的完整列表，请参阅 [Reporting Services 支持的数据源 (SSRS)](create-deploy-and-manage-mobile-and-paginated-reports.md)。

##  <a name="create-a-data-source"></a><a name="bkmk_create_data_source"></a>创建数据源
 若要创建数据源，必须具有以下信息：

-   **数据源类型**连接类型，例如[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 请从连接类型的下拉列表中选择该值。

-   **连接信息** 连接信息包含数据源的名称和位置，以及特定于各数据提供程序的连接属性。 ** “连接字符串”是连接信息的文本表示形式。 例如，如果数据源为某一 SQL Server 数据库，则可以指定该数据库的名称。 对于嵌入数据源，还可以编写在运行时计算的基于表达式的连接字符串。 有关详细信息，请参阅本主题后面部分的 [基于表达式的连接字符串](#bkmk_Expressions_in_connection_strings) 。

-   **凭据** 你提供访问数据所需的凭据。 数据源所有者必须向您授予访问数据源和数据源上特定数据所需的相应权限。 例如，若要连接到网络服务器上安装的 [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 示例数据库，您必须拥有连接到该服务器的权限以及访问该数据库的只读权限。

    > [!NOTE]
    >  在设计上，凭据与数据源是分开管理的。 在本地系统预览报表所使用的凭据可能不同于查看已发布报表所需要的凭据。 在将数据源保存到报表服务器或 SharePoint 站点后，您可能需要更改要从该位置使用的凭据。 有关详细信息，请参阅 [数据源凭据](#bkmk_credentials)。

> [!NOTE]
>  当您在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中创建某个报表的嵌入数据源时，必须在解决方案资源管理器或“报表数据”窗格的报表设计器中创建数据源，但不能在服务器资源管理器中创建。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 报表设计器不支持在服务器资源管理器中创建的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 数据源。

 “报表数据”窗格显示嵌入数据源以及对已添加到报表的共享数据源的引用。 在报表生成器中，共享数据源引用将指向报表服务器或 SharePoint 站点上的共享数据源。 在报表设计器中，共享数据源引用将指向解决方案资源管理器中“共享数据源”文件夹下的某一共享数据源。

##  <a name="credentials-for-data-sources"></a><a name="bkmk_credentials"></a>数据源的凭据
 在设计上，凭据与连接信息可以分开保存和管理。 凭据用于创建数据源、运行数据集查询和预览报表。

> [!NOTE]
>  我们建议您不要包含数据源连接属性的登录信息，例如登录名和密码。 应尽可能将共享数据源与存储凭据一起使用。 在创作环境中，当您创建数据连接或者运行数据集查询时，使用 **“数据源”** 对话框的“凭据”页输入凭据。

 您为从计算机进行数据访问而输入的凭据安全地存储于本地项目配置文件中，并且是特定于您的计算机的。 如果将项目文件复制到另一台计算机，则必须重新为数据源定义凭据。

 在您将某一报表部署到报表服务器或 SharePoint 站点时，其嵌入数据源和共享数据源将独立进行管理。 从您的计算机访问数据所需要的数据源凭据可能不同于从报表服务器访问数据所需要的凭据。

 ![注意](media/rs-fyinote.png "注意")一种很好的做法是在发布报表之后验证数据源连接是否继续成功连接。 如果需要更改凭据，则可以在报表服务器上直接修改。

 若要更改报表使用的数据源，可以在纯模式下修改报表属性，报表管理器或在 SharePoint 模式下从文档库中修改报表属性。 有关详细信息，请参阅以下主题：

-   在[Reporting Services 数据源](report-data/store-credentials-in-a-reporting-services-data-source.md)[的 Reporting Services 数据源存储凭据中存储凭据](report-data/store-credentials-in-a-reporting-services-data-source.md)

-   [为报表数据源指定凭据和连接信息](report-data/specify-credential-and-connection-information-for-report-data-sources.md)

-   [指定用于自定义数据处理扩展插件的连接](report-data/specify-connections-for-custom-data-processing-extensions.md)

-   [在报表生成器中指定凭据](../../2014/reporting-services/specify-credentials-in-report-builder.md)

-   [添加和验证数据连接或数据源 &#40;报表生成器和 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)

##  <a name="common-connection-string-examples"></a><a name="bkmk_connection_examples"></a> 常用连接字符串示例
 连接字符串是数据访问接口的连接属性的文本表示形式。 下表列出了各种数据连接类型的连接字符串示例。

|**数据源**|**示例**|**说明**|
|---------------------|-----------------|---------------------|
|本地服务器上的 SQL Server 数据库|`data source="(local)";initial catalog=AdventureWorks`|将数据源类型设置为 `Microsoft SQL Server`。 有关详细信息，请参阅 [SQL Server 连接类型 (SSRS)](report-data/sql-server-connection-type-ssrs.md)。|
|本地服务器上的 SQL Server 数据库|`data source="(local)";initial catalog=AdventureWorks`|将数据源类型设置为 `Microsoft SQL Server`。|
|SQL Server 实例<br /><br /> database|`Data Source=localhost\MSSQL10_50.InstanceName; Initial Catalog=AdventureWorks`|将数据源类型设置为 `Microsoft SQL Server`。|
|SQL Server Express 数据库|`Data Source=localhost\MSSQL10_50.SQLEXPRESS; Initial Catalog=AdventureWorks`|将数据源类型设置为 `Microsoft SQL Server`。|
|[!INCLUDE[ssSDS](../includes/sssds-md.md)]在云中|`Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True`|将数据源类型设置为 `Azure SQL Database`。 有关详细信息，请参阅 [SQL Azure 连接类型 (SSRS)](report-data/sql-azure-connection-type-ssrs.md)。|
|SQL Server 并行数据仓库|`HOST=<IP address>;database= AdventureWorks; port=<port>`|将数据源类型设置为 `Microsoft SQL Server Parallel Data Warehouse`。 有关详细信息，请参阅 [SQL Server 并行数据仓库连接类型 (SSRS)](report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md)。|
|本地服务器上的 Analysis Services 数据库|`data source=localhost;initial catalog=Adventure Works DW`|将数据源类型设置为 `Microsoft SQL Server Analysis Services`。 有关详细信息，请参阅[针对 MDX 的 Analysis Services 连接类型 (SSRS)](report-data/analysis-services-connection-type-for-mdx-ssrs.md) 或[针对 DMX 的 Analysis Services 连接类型 (SSRS)](report-data/analysis-services-connection-type-for-dmx-ssrs.md)。|
|具有 Sales 透视的 Analysis Services 表格模型数据库|`Data source=<servername>;initial catalog= Adventure Works DW;cube='Sales'`|将数据源类型设置为 `Microsoft SQL Server Analysis Services`。 在 cube= 设置中指定透视名称。 有关详细信息，请参阅 [透视表（SSAS 表格）](https://docs.microsoft.com/analysis-services/tabular-models/perspectives-ssas-tabular)。|
|在本机模式下配置的报表服务器上的报表模型数据源|`Server=http://myreportservername/reportserver; datasource=/models/Adventure Works`|指定报表服务器或文档库 URL 以及报表服务器文件夹或文档库文件夹命名空间中已发布的模型的路径。
|在 SharePoint 集成模式下配置的报表服务器上的报表模型数据源|`Server=http://server; datasource=http://server/site/documents/models/Adventure Works.smdl`|指定报表服务器或文档库 URL 以及报表服务器文件夹或文档库文件夹命名空间中已发布的模型的路径。|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器|`provider=MSOLAP.2;data source=<remote server name>;initial catalog=FoodMart 2000`|将数据源类型设置为 `OLE DB Provider for OLAP Services 8.0`。<br /><br /> 如果将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 属性设置为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，则可以快速连接到 `ConnectTo` 2000 `8.0` 数据源。 若要设置此属性，请使用 **“连接属性”** 对话框中的 **“高级属性”** 选项卡。|
|Oracle 服务器|`data source=myserver`|将数据源类型设置为 `Oracle`。 此外，还必须在报表设计器计算机上和报表服务器上安装 Oracle 客户端工具。 有关详细信息，请参阅 [Oracle 连接类型 (SSRS)](report-data/oracle-connection-type-ssrs.md)。|
|SAP NetWeaver BI 数据源|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|将数据源类型设置为 `SAP NetWeaver BI`。 有关详细信息，请参阅 [SAP NetWeaver BI 连接类型 (SSRS)](report-data/sap-netweaver-bi-connection-type-ssrs.md)。|
|Hyperion Essbase 数据源|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|将数据源类型设置为 `Hyperion Essbase`。 有关详细信息，请参阅 [Hyperion Essbase 连接类型 (SSRS)](report-data/hyperion-essbase-connection-type-ssrs.md)。|
|Teradata 数据源|`data source=`\<NNN>.\<NNN>.\<NNN>.\<NNN>`;`|将数据源类型设置为 `Teradata`。 连接字符串是包含四个字段的 Internet 协议 (IP) 地址，其中每个字段可以包含一至三位数。 有关详细信息，请参阅 [Teradata 连接类型 (SSRS)](report-data/teradata-connection-type-ssrs.md)。|
|XML 数据源、Web 服务|`data source=http://adventure-works.com/results.aspx`|将数据源类型设置为 `XML`。 连接字符串是支持 Web 服务定义语言 (WSDL) 的 Web 服务的 URL。 有关详细信息，请参阅 [XML 连接类型 (SSRS)](report-data/xml-connection-type-ssrs.md)。|
|XML 数据源、XML 文档|`http://localhost/XML/Customers.xml`|将数据源类型设置为 `XML`。 其连接字符串是一个指向 XML 文档的 URL。|
|XML 数据源、嵌入的 XML 文档|*空*|将数据源类型设置为 `XML`。 XML 数据嵌入在报表定义中。|

如果无法使用 `localhost` 连接到报表服务器，请检查是否已启用网络协议 TCP/IP 协议。 有关详细信息，请参阅 [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md)。

##  <a name="special-characters-in-a-password"></a><a name="bkmk_special_password_characters"></a>密码中的特殊字符
 如果将 ODBC 或 SQL 数据源配置为提示输入密码或在连接字符串中包含密码，并且用户输入了具有标点符号等特殊字符的密码，则有些基础数据源驱动程序无法验证特殊字符。 处理报表时，可能会出现“密码无效”这一消息来指示此问题。 如果不能更改密码，则可以使用数据库管理员角色将相应的凭据作为系统 ODBC 数据源名称 (DSN) 的一部分存储在服务器上。 有关详细信息，请参阅 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK 文档中的“OdbcConnection.ConnectionString”。

##  <a name="expression-based-connection-strings"></a><a name="bkmk_Expressions_in_connection_strings"></a>基于表达式的连接字符串
 基于表达式的连接字符串是在运行时计算的。 例如，您可以将数据源指定为参数，在连接字符串中包含相应的参数引用，并允许用户选择报表的数据源。 例如，假设一个跨国公司在多个国家/地区都配置了数据服务器。 使用基于表达式的连接字符串，要运行销售报表的用户就可以在运行报表之前选择用于特定国家/地区的数据源。

 下面的示例说明了 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 连接字符串中数据源表达式的用法。 该示例假设您已经创建了一个名为 `ServerName`的报表参数：

```
="data source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks"
```

 数据源表达式在运行时或预览报表时进行处理。 此类表达式必须用 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]编写。 定义数据源表达式时请遵循以下原则：

-   使用静态连接字符串设计报表。 静态连接字符串指的是不通过表达式设置的连接字符串（例如，按照步骤创建报表特定数据源或共享数据源时，定义的就是静态连接字符串）。 使用静态连接字符串，可以在报表设计器中连接到数据源，以便获取创建报表所需的查询结果。

-   定义数据源连接时，请不要使用共享数据源。 不能在共享数据源中使用数据源表达式。 您必须为报表定义嵌入数据源。

-   在连接字符串之外单独指定凭据。 您可以使用存储的凭据、提示凭据或集成安全性。

-   添加报表参数以指定数据源。 对于参数值，可以提供可用值的静态列表（这种情况下，可用值应该是报表可以使用的数据源），或定义在运行时检索数据源列表的查询。

-   请确保列表中的数据源共用同一个数据库架构。 所有报表设计都以架构信息为基础。 如果用于定义报表的架构和报表运行时使用的实际架构不相符，报表将可能无法运行。

-   在发布报表之前，使用表达式替换静态连接字符串。 使用表达式替换静态连接字符串之前，必须保证已经完成了报表的设计。 一旦使用了表达式，就不能在报表设计器中执行查询。 此外，“报表数据”窗格中的字段列表以及“参数”列表将不会自动更新。

## <a name="see-also"></a>另请参阅
 [嵌入和共享的数据连接或数据源 &#40;报表生成器和 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) [管理报表数据源](report-data/manage-report-data-sources.md) ["数据源属性" 对话框、"凭据](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md)[共享数据源属性" 对话框、](../../2014/reporting-services/shared-data-source-properties-dialog-box-credentials.md) "凭据" "[创建"、"修改" 和 "删除共享数据源" &#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md) [设置部署属性 &#40;Reporting Services](tools/set-deployment-properties-reporting-services.md)&#41;[指定报表数据源的凭据和连接信息](report-data/specify-credential-and-connection-information-for-report-data-sources.md)&#40;[报表生成器和 SSRS](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)&#41;
