---
title: 报表数据
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: reporting-services-2014, sql-server-2014
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 8c0a6ef25f33b5396ecea36edfd57ac3c42e8f5b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721414"
---
# <a name="report-data-in-sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS) 中的报表数据

  报表数据可以来自您的组织中的多种数据源。 设计报表的第一步是创建表示基础报表数据的数据源和数据集。 每个数据源都包含数据连接信息。 每个数据集都包含一个查询命令，该命令定义要用作来自数据源的数据的字段集。 若要展现来自各数据集的数据，请添加表、矩阵、图表或地图之类的数据区域。 处理报表时，将对数据源运行查询，并且每个数据区域都可以根据需要进行扩展，以便显示数据集的查询结果。  
  
##  <a name="BkMk_ReportDataTerms"></a> 术语

 如果您不熟悉[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]概念，查看中的以下条款[Reporting Services 概念&#40;SSRS&#41;](../reporting-services-concepts-ssrs.md):*数据连接*，*嵌入的数据源*，*共享数据源*，*嵌入数据集*，*共享数据集*，*数据集查询**报表部件*，并*数据警报*。  
  
##  <a name="BkMk_ReportDataTips"></a> 用于指定报表数据的提示

 使用以下信息可以设计您的报表数据策略。  
  
- **数据源** 可以独立于报表服务器或 SharePoint 站点上的报表单独发布和管理数据源。 对于每个数据源，您或数据库所有者可以在一个位置中管理连接信息。 数据源凭据安全地存储在报表服务器上；请不要在连接字符串中包括密码。 您可以将来自测试服务器的数据源重定向到生产服务器。 您可以禁用某一数据源，以便挂起使用它的所有报表。 有关支持的数据源的列表，请参阅[数据连接、 数据源和 Reporting Services 中的连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
- **数据集** 可以独立于数据集所依赖的报表或共享数据源来单独发布和管理数据集。 您或数据库所有者可以提供优化的查询以便报表作者使用。 当您更改查询时，使用共享数据集的所有报表都将使用更新的查询。 您可以启用数据集缓存来提高性能。 您可以安排在特定时间进行查询缓存，或使用共享的计划。  
  
- **报表部件使用的数据** 报表部件可以包含它们所依赖的数据。 有关报表部件的详细信息，请参阅[报表设计器中的报表部件 (SSRS)](../report-design/report-parts-in-report-designer-ssrs.md)。  
  
- **筛选数据** 可以在查询中或报表中筛选报表数据。 您可以使用数据集和查询变量来创建级联参数，并且使用户能够将成千上万种选择缩减为更为可控的数目。 您可以基于参数值或者您指定的其他值来筛选表或图表中的数据。  
  
- **参数** 包含查询变量的数据集查询命令将自动创建匹配的报表参数。 也可以手动创建参数。 当您查看报表时，报表工具栏将显示这些参数。 用户可以选择值，以便控制报表数据或报表外观。 若要为特定用户自定义报表数据，您可以创建具有链接到相同报表定义的不同默认值的报表参数集，或者使用内置的 `UserID` 字段。 有关详细信息，请参阅[报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)和[表达式中的内置集合（报表生成器和 SSRS）](../report-design/built-in-collections-in-expressions-report-builder.md)。  
  
- **数据警报** 在发布报表后，您可以基于报表数据创建警报，并且在警报满足您指定的规则时接收电子邮件。  
  
- **对数据进行分组和聚合** 可在查询或报表中对报表数据进行分组和聚合。 如果您聚合查询中的值，则可以继续在有意义的约束内合并报表中的值。  有关详细信息，请参阅[对数据进行筛选、分组和排序（报表生成器和 SSRS）](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)和[聚合函数（报表生成器和 SSRS）](../report-design/report-builder-functions-aggregate-function.md)。  
  
- **对数据排序** 可以在查询中或报表中对报表数据排序。 在表中，您还可以添加交互排序按钮，以便让用户控制排序顺序。  
  
- **基于表达式的数据** 因为大多数报表属性可以是基于表达式的，并且表达式可以包含对数据集字段和报表参数的引用，所以，可以编写功能强大的表达式来控制报表数据和外观。 您可以通过定义参数，使用户能够控制其所看到的数据。  
  
- **显示来自一个数据集的数据** 来自一个数据集的数据通常显示在一个或多个数据区域中，例如表和图表。  
  
- **显示来自多个数据集的数据**  可以在数据区域中基于一个数据集编写表达式，用于查找其他数据集中的值或聚合。 您可以基于一个数据集在表中包含子报表，以便显示来自其他数据源的数据。  
  
## <a name="data-connections-data-sources-and-datasets"></a>数据连接、数据源和数据集

 使用以下列表可帮助定义报表的数据源。  
  
- 考虑是否使用嵌入的或共享的数据源和数据集。 与数据源的所有者协作，以便实现并使用适用于您的组织的身份验证和授权技术。  
  
- 了解您的组织的软件数据层体系结构以及从数据类型导致的潜在问题。 了解数据扩展插件和数据处理扩展插件是如何影响查询结果的。 数据类型在数据源、数据访问接口以及在报表定义 (.rdl) 文件中存储的数据类型之间是不同的。  
  
- 了解 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 客户端/服务器体系结构和工具。 例如，在报表设计器中，您在使用内置数据源类型的客户端计算机上创作报表。 在您发布报表时，在报表服务器或 SharePoint 站点上必须支持数据源类型。  有关详细信息，请参阅 [Reporting Services 支持的数据源 (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
- 数据源和数据集在报表中创作，并且从客户端创作工具发布到报表服务器或 SharePoint 站点。 可以直接在报表服务器上创建数据源。 在发布后，您可以在报表服务器上配置凭据和其他属性。 有关详细信息，请参阅[数据连接、 数据源和 Reporting Services 中的连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)并[Reporting Services 工具](../tools/reporting-services-tools.md)。  
  
- 您可以使用的数据源取决于所安装的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 数据扩展插件。 对数据源的支持可能会因客户端创作工具、报表服务器版本和报表服务器平台而异。 有关详细信息，请参阅 [Reporting Services 支持的数据源 (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
- 基于数据源类型以及是在您的客户端还是报表服务器或 SharePoint 站点查看报表的，数据源凭据将会有所不同。 有关详细信息，请参阅[在 SharePoint 网站上为报表服务器项设置权限（SharePoint 集成模式中的 Reporting Services）](../security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)、[为报表数据源指定凭据和连接信息](../../integration-services/connection-manager/data-sources.md)和 [Reporting Services 工具](../tools/reporting-services-tools.md)中特定于每个工具的凭据信息。  
  
## <a name="related-tasks"></a>Related Tasks

 与创建数据连接以及从外部数据源、数据集和查询添加数据相关的任务。  
  
|||  
|-|-|  
|**常见任务**|**链接**|  
|创建数据连接|[报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|创建数据集和查询|[报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|  
|在发布后管理数据源|[管理报表数据源](manage-report-data-sources.md)|  
|在发布后管理共享数据集|[管理共享数据集](manage-shared-datasets.md)|  
|创建和管理数据警报|[Reporting Services 数据警报](../tutorial-creating-a-basic-table-report-report-builder.md)|  
|缓存共享数据集|[缓存共享数据集 (SSRS)](../report-server/cache-shared-datasets-ssrs.md)|  
|计划要预加载缓存的共享数据集|[计划](../subscriptions/schedules.md)|  
|添加数据扩展插件|[实现数据处理扩展插件](../extensions/data-processing/implementing-a-data-processing-extension.md)|