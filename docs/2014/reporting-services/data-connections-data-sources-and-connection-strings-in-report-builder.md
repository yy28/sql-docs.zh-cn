---
title: 数据连接、 数据源和报表生成器中的连接字符串 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10421"
ms.assetid: 7e103637-4371-43d7-821c-d269c2cc1b34
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 13edc28a739af6a40ab47766c1909be3a8105ee5
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288865"
---
# <a name="data-connections-data-sources-and-connection-strings-in-report-builder"></a>报表生成器中的数据连接、数据源和连接字符串
  为了在报表中包含数据，您需要创建数据连接和数据集。 数据连接包括有关如何访问外部数据源的信息。 数据集包含一个查询命令，用于指定通过使用数据连接要包含哪些数据。  
  
1.  **“报表数据”窗格中的数据源** 在创建嵌入数据源或添加共享数据源后，会在“报表数据”窗格中显示一个数据源。  
  
2.  **“连接”对话框** 使用“连接”对话框可以生成连接字符串或粘贴连接字符串。  
  
3.  **数据连接信息** 将连接字符串传递给数据扩展插件。  
  
4.  **凭据** 凭据与连接字符串是分开管理的。  
  
5.  **数据扩展插件/数据访问接口** 对数据的连接可通过多个数据访问层。  
  
6.  **外部数据源** 检索来自关系数据库、多维数据库、SharePoint 列表、Web 服务或报表模型的数据。  
  
 有关详细信息，请参阅[嵌入和共享的数据连接或数据源&#40;报表生成器和 SSRS&#41; ](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)并[数据连接、 数据源和 Reporting Services中的连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 通过使用预定义的共享数据源、共享数据集和报表部件，也可以将数据包含在报表中。 这些项已具有您所需的数据连接信息。 有关详细信息，请参阅[向报表添加数据&#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 ![rs_DataSourcesStory](media/rs-datasourcesstory.gif "rs_DataSourcesStory")  
  
##  <a name="ConnectionString"></a> 连接字符串示例  
 数据连接包括一个连接字符串，它通常由外部数据源的所有者提供。 下表列出了不同外部数据源类型的连接字符串示例：  
  
|**数据源**|**示例**|**说明**|  
|---------------------|-----------------|---------------------|  
|本地服务器上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库|`data source="(local)";initial catalog=AdventureWorks2012`|将数据源类型设置为 `SQL Server`。|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例数据库|`Data Source=localhost\MSSQL12.InstanceName; Initial Catalog= AdventureWorks2012`|将数据源类型设置为 `SQL Server`。|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express 数据库|`Data Source=localhost\MSSQL12.SQLEXPRESS; Initial Catalog= AdventureWorks2012`|将数据源类型设置为 `SQL Server`。|  
|本地服务器上的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库|`data source=localhost;initial catalog=Adventure Works DW 2012`|将数据源类型设置为 `SQL Server Analysis Services`。|  
|SharePoint 列表|`data source=http://MySharePointWeb/MySharePointSite/`|将数据源类型设置为 `SharePoint List`。|  
||||  
|报表模型|不适用。|报表模型不需要连接字符串。 在报表生成器中，找到报表服务器并选择表示报表模型的 .smdl 文件。|  
|Oracle 服务器|`data source=myserver`|将数据源类型设置为 `Oracle`。 必须在报表生成器计算机上和报表服务器上安装 Oracle 客户端工具。|  
|SAP NetWeaver BI 数据源|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|将数据源类型设置为 `SAP NetWeaver BI`。|  
|Hyperion Essbase 数据源|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|将数据源类型设置为 `Hyperion Essbase`。|  
|Teradata 数据源|`data source=` *\<NN>.\<NNN>.\<NNN>.\<N>* `;`|将数据源类型设置为 `Teradata`。 连接字符串是包含四个字段的 Internet 协议 (IP) 地址，其中每个字段可以包含一至三位数。|  
|Teradata 数据源|`Database=` *\<database name>* `; data source=` *\<NN*N *>.\<NNN>.\<NNN>.\<N*NN*>*`;Use X Views=False;Restrict to Default Database=True`|与前一示例类似，将数据源类型设置为 `Teradata`。 请仅使用在 Database 标记中指定的默认数据库，不要自动发现数据关系。|  
|XML 数据源、Web 服务|`data source=http://adventure-works.com/results.aspx`|将数据源类型设置为 `XML`。 连接字符串是支持 Web 服务定义语言 (WSDL) 的 Web 服务的 URL。|  
|XML 数据源、XML 文档|`http://localhost/XML/Customers.xml`|将数据源类型设置为 `XML`。 其连接字符串是一个指向 XML 文档的 URL。|  
|XML 数据源、嵌入的 XML 文档|*Empty*|将数据源类型设置为 `XML`。 XML 数据嵌入在报表定义中。|  
  
 有关每种连接类型的详细信息，请参阅[从外部数据源中添加数据&#40;SSRS&#41; ](report-data/add-data-from-external-data-sources-ssrs.md)并[支持的 Reporting Services 数据源&#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  

  
##  <a name="Creating"></a> 创建数据源  
 若要创建嵌入数据源，您必须具有一个连接字符串和访问数据所需的凭据。 此信息通常来自数据源的所有者。 数据连接作为数据源的一部分保存在报表定义中。 凭据和连接是分开管理的。 有关分步说明，请参阅[添加和验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  某些类型的凭据可能只支持报表生成器使用的一部分情形，而全部情形包括：在查询设计器中运行查询、未连接到报表服务器时从您的计算机预览报表以及从报表服务器运行报表。 建议您尽量使用共享数据源。 可以在报表服务器上存储共享数据源的凭据。 有关详细信息，请参阅 [在报表生成器中指定凭据](../../2014/reporting-services/specify-credentials-in-report-builder.md)。  
  
 若要创建共享的数据源，您必须使用报表管理器直接在报表服务器上创建数据源，或使用诸如报表设计器中的创作环境[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。 有关详细信息，请参阅[创建嵌入或共享数据源&#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md)。  
  

  
## <a name="see-also"></a>请参阅  
 [向报表添加数据&#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [报表部件（报表生成器和 SSRS）](report-parts-report-builder-and-ssrs.md)  
  
  
