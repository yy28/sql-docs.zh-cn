---
title: 创建数据连接字符串 - 报表生成器和 SSRS | Microsoft Docs
ms.date: 11/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 73bf9e24ffb42ef93547097c53b5838a22292fda
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "74190913"
---
# <a name="create-data-connection-strings---report-builder--ssrs"></a>创建数据连接字符串 - 报表生成器和 SSRS

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  若要在[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中添加数据，必须先创建连接到数据源的连接字符串。 本文介绍了如何创建数据连接字符串，以及与数据源凭据相关的重要信息。 数据源包含数据源类型、连接信息以及要使用的凭据的类型。 有关更多背景信息，请参阅 [SQL Server Reporting Services (SSRS) 中的报表数据简介](report-data-ssrs.md)。
  
##  <a name="built-in-data-extensions"></a><a name="bkmk_DataConnections"></a> 内置数据扩展插件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的默认数据扩展插件包括 Microsoft SQL Server、Microsoft Azure SQL 数据库和 Microsoft SQL Server Analysis Services。 有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支持的数据源和版本的完整列表，请参阅 [Reporting Services 支持的数据源 (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
##  <a name="common-connection-string-examples"></a><a name="bkmk_connection_examples"></a> 常用连接字符串示例  
 连接字符串是数据访问接口的连接属性的文本表示形式。 下表列出了各种数据连接类型的连接字符串示例。  
 
 > [!NOTE]  
>  访问[Connectionstrings.com](https://www.connectionstrings.com/) 是可获取连接字符串示例的另一种方法。 
  
|**数据源**|**示例**|**说明**|  
|---------------------|-----------------|---------------------|  
|本地服务器上的 SQL Server 数据库|`data source="(local)";initial catalog=AdventureWorks`|将数据源类型设置为 **Microsoft SQL Server**。 有关详细信息，请参阅 [SQL Server 连接类型 (SSRS)](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)。|  
|SQL Server 实例<br /><br /> database|`Data Source=localhost\MSSQL13.<InstanceName>; Initial Catalog=AdventureWorks`|将数据源类型设置为 **Microsoft SQL Server**。|  
|Azure SQL 数据库|`Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True`|将数据源类型设置为“Microsoft Azure SQL 数据库”  。 有关详细信息，请参阅 [SQL Azure 连接类型 (SSRS)](../../reporting-services/report-data/sql-azure-connection-type-ssrs.md)。|  
|SQL Server 并行数据仓库|`HOST=<IP address>;database= AdventureWorks; port=<port>`|将数据源类型设置为 **Microsoft SQL Server Parallel Data Warehouse**。 有关详细信息，请参阅 [SQL Server 并行数据仓库连接类型 (SSRS)](../../reporting-services/report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md)。|  
|本地服务器上的 Analysis Services 数据库|`data source=localhost;initial catalog=Adventure Works DW`|将数据源类型设置为 **Microsoft SQL Server Analysis Services**。 有关详细信息，请参阅[针对 MDX 的 Analysis Services 连接类型 (SSRS)](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md) 或[针对 DMX 的 Analysis Services 连接类型 (SSRS)](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)。|  
|具有 Sales 透视的 Analysis Services 表格模型数据库|`Data source=<servername>;initial catalog= Adventure Works DW;cube='Sales'`|将数据源类型设置为 **Microsoft SQL Server Analysis Services**。 在 cube= 设置中指定透视名称。 有关详细信息，请参阅 [透视表（SSAS 表格）](https://docs.microsoft.com/analysis-services/tabular-models/perspectives-ssas-tabular)。|  
|Oracle 服务器|`data source=myserver`|将数据源类型设置为 **Oracle**。 此外，还必须在报表设计器计算机上和报表服务器上安装 Oracle 客户端工具。 有关详细信息，请参阅 [Oracle 连接类型 (SSRS)](../../reporting-services/report-data/oracle-connection-type-ssrs.md)。|  
|SAP NetWeaver BI 数据源|`DataSource=https://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|将数据源类型设置为 **SAP NetWeaver BI**。 有关详细信息，请参阅 [SAP NetWeaver BI 连接类型 (SSRS)](../../reporting-services/report-data/sap-netweaver-bi-connection-type-ssrs.md)。|  
|Hyperion Essbase 数据源|`Data Source=https://localhost:13080/aps/XMLA; Initial Catalog=Sample`|将数据源类型设置为 **Hyperion Essbase**。 有关详细信息，请参阅 [Hyperion Essbase 连接类型 (SSRS)](../../reporting-services/report-data/hyperion-essbase-connection-type-ssrs.md)。|  
|Teradata 数据源|`data source=`\<NNN>.\<NNN>.\<NNN>.\<NNN>`;`|将数据源类型设置为 **Teradata**。 连接字符串是包含四个字段的 Internet 协议 (IP) 地址，其中每个字段可以包含一至三位数。 有关详细信息，请参阅 [Teradata 连接类型 (SSRS)](../../reporting-services/report-data/teradata-connection-type-ssrs.md)。|  
|Teradata 数据源|`Database=` *database name>\<* `; data source=` *NN\<* N *>.\<NNN>.\<NNN>.\<NNN* *>* `;Use X Views=False;Restrict to Default Database=True`|与前一示例类似，将数据源类型设置为 **Teradata**。 请仅使用在 Database 标记中指定的默认数据库，不要自动发现数据关系。|  
|XML 数据源、Web 服务|`data source=https://adventure-works.com/results.aspx`|将数据源类型设置为 **XML**。 连接字符串是支持 Web 服务定义语言 (WSDL) 的 Web 服务的 URL。 有关详细信息，请参阅 [XML 连接类型 (SSRS)](../../reporting-services/report-data/xml-connection-type-ssrs.md)。|  
|XML 数据源、XML 文档|`https://localhost/XML/Customers.xml`|将数据源类型设置为 **XML**。 其连接字符串是一个指向 XML 文档的 URL。 
|XML 数据源、嵌入的 XML 文档|*Empty*|将数据源类型设置为 **XML**。 XML 数据嵌入在报表定义中。|  
|SharePoint 列表|`data source=https://MySharePointWeb/MySharePointSite/`|将数据源类型设置为 **SharePoint List**。|  
| Power BI Premium 数据集（自 Reporting Services 2019 起） | Server=powerbi://api.powerbi.com/v1.0/myorg/<workspacename>;initial catalog = <YourDatasetName> | 将数据源类型设置为 **Microsoft SQL Server Analysis Services**。 |

  
 如果无法使用 **localhost**连接到报表服务器，请检查是否已启用网络协议 TCP/IP 协议。 有关详细信息，请参阅 [Configure Client Protocols](../../database-engine/configure-windows/configure-client-protocols.md)。  
  
 若要详细了解连接到这些数据源类型所需的配置，请参阅[添加外部数据源中的数据 &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) 或 [Reporting Services 支持的数据源 &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) 下的特定数据连接文章。  
  
##  <a name="special-characters-in-a-password"></a><a name="bkmk_special_password_characters"></a> 密码中的特殊字符  
 如果将 ODBC 或 SQL 数据源配置为提示输入密码或在连接字符串中包含密码，并且用户输入了具有标点符号等特殊字符的密码，则有些基础数据源驱动程序无法验证特殊字符。 处理报表时，可能会出现“密码无效”这一消息来指示此问题。 如果不能更改密码，则可以使用数据库管理员角色将相应的凭据作为系统 ODBC 数据源名称 (DSN) 的一部分存储在服务器上。 有关详细信息，请参阅 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 文档中的“[OdbcConnection.ConnectionString](https://docs.microsoft.com/dotnet/api/system.data.odbc.odbcconnection.connectionstring)”。  
  
##  <a name="expression-based-connection-strings"></a><a name="bkmk_Expressions_in_connection_strings"></a> 基于表达式的连接字符串  
 基于表达式的连接字符串是在运行时计算的。 例如，您可以将数据源指定为参数，在连接字符串中包含相应的参数引用，并允许用户选择报表的数据源。 例如，假设一个跨国公司在多个国家/地区都配置了数据服务器。 使用基于表达式的连接字符串，要运行销售报表的用户就可以在运行报表之前选择用于特定国家/地区的数据源。  
  
 下面的示例说明了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接字符串中数据源表达式的用法。 该示例假设您已经创建了一个名为 `ServerName`的报表参数：  
  
```  
="data source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks"  
```  
  
 数据源表达式在运行时或预览报表时进行处理。 此类表达式必须用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]编写。 定义数据源表达式时请遵循以下原则：  
  
-   使用静态连接字符串设计报表。 静态连接字符串指的是不通过表达式设置的连接字符串（例如，按照步骤创建报表特定数据源或共享数据源时，定义的就是静态连接字符串）。 使用静态连接字符串，可以在报表设计器中连接到数据源，以便获取创建报表所需的查询结果。  
  
-   定义数据源连接时，请不要使用共享数据源。 不能在共享数据源中使用数据源表达式。 您必须为报表定义嵌入数据源。  
  
-   在连接字符串之外单独指定凭据。 您可以使用存储的凭据、提示凭据或集成安全性。  
  
-   添加报表参数以指定数据源。 对于参数值，可以提供可用值的静态列表（这种情况下，可用值应该是报表可以使用的数据源），或定义在运行时检索数据源列表的查询。  
  
-   请确保列表中的数据源共用同一个数据库架构。 所有报表设计都以架构信息为基础。 如果用于定义报表的架构和报表运行时使用的实际架构不相符，报表将可能无法运行。  
  
-   在发布报表之前，使用表达式替换静态连接字符串。 使用表达式替换静态连接字符串之前，必须保证已经完成了报表的设计。 一旦使用了表达式，就不能在报表设计器中执行查询。 此外，“报表数据”窗格中的字段列表以及“参数”列表将不会自动更新。  

## <a name="next-steps"></a>后续步骤

[SQL Server Reporting Services (SSRS) 中的报表数据简介](report-data-ssrs.md)
[创建和修改共享数据源](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
[创建和修改嵌入的数据源](../../reporting-services/report-data/create-and-modify-embedded-data-sources.md)   
[设置部署属性](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
[为报表数据源指定凭据和连接信息](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)
