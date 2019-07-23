---
title: 从外部数据源中添加数据 (SSRS) | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
reviewer: ''
ms.custom: ''
ms.date: 03/17/2017
ms.openlocfilehash: 3ec3fe9ba7641a7c60b3035ff6dc5e11cdfe3691
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68251255"
---
# <a name="add-data-from-external-data-sources-ssrs"></a>从外部数据源中添加数据 (SSRS)
  若要从外部数据源中检索数据，您需要使用数据连接。 数据连接信息通常由外部数据源的所有者提供，该所有者负责授予权限并指定要使用的凭据类型。 数据连接信息另存为报表数据源。 数据源类型指定要用于检索数据的数据扩展插件。  
  
 有关数据源类型的详细信息，请参阅 [本节内容](#InThisSection)。  
  
##  <a name="DataAccess"></a> 了解数据访问技术  
 检索报表数据集的数据需要数据访问软件的多个层。 下面的列表简单说明了如何将报表与数据访问技术一起使用：  
  
-   **应用程序和用户界面** ：用于执行以下操作的报表生成器应用程序：创建数据源、添加对共享数据源的引用、添加共享数据集，或者添加包括数据源的报表部件和该应用程序所依赖的数据集。  
  
-   **报表定义元素** 数据源和数据集是报表定义的一部分。 在将报表发布到报表服务器之后，将根据报表定义单独管理共享数据源和共享数据集。  
  
    -   **数据源和共享数据源** 报表定义中包括数据处理扩展插件的类型信息、连接信息和身份验证信息的那一部分。  
  
    -   **数据集和字段集合** 报表定义中包括查询、字段集合和字段数据类型的那一部分。  
  
-   **Reporting Services 数据扩展插件** 随报表生成器一起安装的内置数据扩展插件。 数据扩展插件提供用于处理身份验证、服务器聚合和多值参数的功能。  
  
-   **数据访问接口** 用于管理与外部数据源连接并从中检索数据的软件。 数据访问接口定义连接字符串语法。 大部分数据扩展插件都是构建在数据访问接口层之上的。  
  
-   **外部数据源** 要从中检索报表数据的位置，例如，数据库、文件、多维数据集或 Web 服务。  
  
> [!NOTE]  
>  在您未连接到报表服务器时，您可以从随报表生成器一起安装的数据扩展插件中进行选择。 您作为单个用户使用您计算机上的凭据访问数据。 在您连接到报表服务器时，您可以从报表服务器上安装的数据扩展插件中进行选择。 您以运行报表的多个用户中的一个用户名义访问数据，并且您使用的是报表服务器上的凭据。 有关详细信息，请参阅[为报表数据源指定凭据和连接信息](specify-credential-and-connection-information-for-report-data-sources.md)  
  
##  <a name="ReportData"></a> 了解报表数据  
 用最简单的形式来说，报表将来自报表数据集的数据显示在报表页上的数据区域中，即，显示在单个表、图表、矩阵或其他类型的报表数据区域中。 报表数据集中的数据来自于单个查询命令返回的第一个结果集，该查询命令是通过对外部数据源进行只读访问运行的。 可以根据需要扩展每个数据区域以显示数据集中的所有数据。  
  
 数据集中的数据实质上是表格。 列来自于数据集查询中的字段。 行来自于结果集中的行。 可以在报表中使用以下通用数据类型：  
  
-   矩形数据。 每一行中列编号相同的结果集中的数据。  
  
-   分层数据作为平展行集予以支持。  
  
    -   不支持每一数据行的列编号不同的不规则层次结构。 对于某些数据扩展插件，这具有一些意义。  
  
    -   使用多维数据源的数据扩展插件使用 XML for Analysis 协议并将数据作为平展行集进行检索，而非作为单元集。  
  
    -   XML 数据扩展插件自动平展 XML 数据以将其用在报表中。 如果 XML 元素的第一个实例不包含所有特性或子元素，则这些数据可能不能用作报表数据。  
  
-   支持递归数据。 一个包含递归数据层次结构的结果集会包括有关矩形结果集中分层结构的所有信息。 例如，公司中的上下级结构可用一个包含“员工”和“经理”两列的表来表示。 每位经理同时也是另一位经理的员工。 总经理通常包含一个 null 或某个其他指示该员工没有经理的标识符。  
  
  
##  <a name="DataTypes"></a> 使用数据类型  
 创建数据集后，字段的数据类型将从 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]映射到公共语言运行时 (CLR) 数据类型的子集。 无法清晰映射的数据类型以字符串的形式返回。 有关使用字段数据类型的详细信息，请参阅 [数据集字段集合（报表生成器和 SSRS）](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)。 创建参数后，数据类型必须是受支持的报表定义数据类型。 有关将数据类型从数据提供程序映射到报表参数的详细信息，请参阅[表达式中的数据类型（报表生成器和 SSRS）](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)。  
  
  
##  <a name="HowTo"></a> 操作指南主题  
 本节包含使用数据连接、数据源和数据集的分步说明。  
  
 [添加和验证数据连接（报表生成器和 SSRS）](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [创建共享数据集或嵌入数据集（报表生成器和 SSRS）](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [向数据集添加筛选器（报表生成器和 SSRS）](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="InThisSection"></a> 本节内容  
 下列主题提供有关每个内置数据扩展插件的信息。  
  
|主题|数据源类型|  
|-----------|----------------------|  
|[SQL Server 连接类型 (SSRS)](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|[针对 MDX 的 Analysis Services 连接类型 (SSRS)](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[PowerPivot 连接类型 (SSRS)](../../reporting-services/report-data/power-pivot-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[SharePoint 列表连接类型 (SSRS)](../../reporting-services/report-data/sharepoint-list-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 列表|  
|[SQL Azure 连接类型 (SSRS)](../../reporting-services/report-data/sql-azure-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|[SQL Server 并行数据仓库连接类型 (SSRS)](../../reporting-services/report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|  
|[SAP NetWeaver BI 连接类型 (SSRS)](../../reporting-services/report-data/sap-netweaver-bi-connection-type-ssrs.md)|SAP NetWeaver BI|  
|[Hyperion Essbase 连接类型 (SSRS)](../../reporting-services/report-data/hyperion-essbase-connection-type-ssrs.md)|Hyperion Essbase|  
|[OLE DB 连接类型 (SSRS)](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)|OLE DB|  
|[ODBC 连接类型 (SSRS)](../../reporting-services/report-data/odbc-connection-type-ssrs.md)|ODBC|  
|[XML 连接类型 (SSRS)](../../reporting-services/report-data/xml-connection-type-ssrs.md)|XML|  
  
##  <a name="Related"></a> 相关章节

 文档中的这些章节提供有关报表数据的深入概念性信息，以及有关如何定义、自定义和使用与数据相关的报表部件的步骤信息。  
  
|主题|描述|  
|-----------|-----------------|  
|[报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)|提供访问报表数据的概述。|  
|[报表生成器中的数据连接、数据源和连接字符串](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)|提供有关数据连接和数据源的信息。|  
|[报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|提供有关嵌入数据集和共享数据集的信息。|  
|[数据集字段集合（报表生成器和 SSRS）](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)|提供有关查询生成的数据集字段集合的信息。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [联机丛书](https://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS) ](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。|提供有关每个数据扩展插件的平台和版本支持的详细信息。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][联机丛书](https://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文档中的[数据处理扩展插件概述](../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)。|为高级用户提供有关数据扩展插件的详细信息。|  
  
  
## <a name="see-also"></a>另请参阅  
 [报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [查询设计工具 (SSRS)](query-design-tools-ssrs.md)  
  
  
