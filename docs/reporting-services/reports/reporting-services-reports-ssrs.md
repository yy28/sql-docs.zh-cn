---
title: Reporting Services 报表 (SSRS) | Microsoft Docs
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, report creation
ms.assetid: 52ed9e74-f2c8-488b-a2c2-6dfbc2a2c8cc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b872952b1e84bfc12722e14234207ff67525699b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571022"
---
# <a name="reporting-services-reports-ssrs"></a>Reporting Services 报表 (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表是基于 XML 的报表定义，其中包括报表数据和报表布局元素。 在客户端文件系统中，报表定义具有文件扩展名 .rdl。 在发布某一分页报表后，该报表将成为在报表服务器或 SharePoint 站点上存储的报表项。 分页报表是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]提供的基于服务器的报表平台的一部分。 你还可以 [Create mobile reports with SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)。  
  
 如果你不熟悉 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，请务必查阅 [Reporting Services 概念 (SSRS)](../../reporting-services/reporting-services-concepts-ssrs.md) 中的信息。  
  
## <a name="benefits-of-reporting-services-paginated-reports"></a>Reporting Services 分页报表的优点  
 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表解决方案完成以下任务：  
  
-   使用提供单个事实版本的一组数据源。 在这些数据源的基础上建立报表，以便提供统一的数据视图来帮助作出业务决策。  
  
-   通过使用数据区域，以多种互连的方式展现您的数据。 显示在表、矩阵或交叉表中组织的数据，展开/折叠组、图表、仪表、指示器或 KPI 和地图，并且能够在表中嵌套图表。  
  
-   查看报表以便供您自己使用，或者将报表发布到报表服务器或 SharePoint 站点，以便与您的团队或组织共享。  
  
-   定义报表一次，并且以不同方式显示该报表。 您可以将报表导出到多种文件格式，或者将报表以电子邮件的形式传递到订阅服务器或传递到共享文件。 您可以创建多个链接的报表，这些报表将单独的参数集应用于相同的报表定义。  
  
-   使用报表部件、共享数据源、共享查询和子报表可以定义数据可视化以便重复使用。  
  
-   将报表数据源与报表定义分开管理。 例如，您可以不必更改报表，就从测试数据源更改为生产数据源。  
  
-   以自由格式布局设计报表。 报表布局不受到信息组的限制。 您可以通过可提高对数据的理解、洞察和操作的形式来组织页面上的数据显示。  
  
-   启用钻取操作、展开/折叠切换、排序按钮、工具提示和报表参数，以便使报表读者能够与报表交互。 将报表参数与您编写的表达式结合使用，使报表读者能够控制对数据进行筛选、分组和排序的方式。  
  
-   定义表达式，使您能够自定义对报表数据进行筛选、分组和排序的方式。  
  
 ![rs_GettingStartedReport](../../reporting-services/report-builder/media/rs-gettingstartedreport.png "rs_GettingStartedReport")  
  
##  <a name="bkmk_StagesSummary"></a> 报表处理的阶段  
 在您创建报表时，以 XML 格式定义一个报表定义文件 (.rdl)。 该文件包含报表处理器合并报表数据和报表布局所需的所有信息。 当您查看报表时，报表将经历以下阶段：  
  
-   **编译。** 对报表定义中的表达式进行计算，将编译后的中间格式内部存储于报表服务器上。  
  
-   **处理。** 运行数据集查询，并且将中间格式与数据和布局合并在一起。  
  
-   **呈现。** 将处理后的报表发送到呈现扩展插件，以便确定每页上适合多少信息并创建分页的报表。  
  
-   **导出（可选）。** 将报表导出为不同的文件格式。  
  
 有关详细信息，请参阅 [Reporting Services 概念 (SSRS)](../../reporting-services/reporting-services-concepts-ssrs.md) 中的[报表的阶段](../../reporting-services/reporting-services-concepts-ssrs.md#bkmk_StagesofReports)。  
  
## <a name="create-paginated-reports"></a>创建分页报表  
 创建分页报表：  
  
-   **确定报表的用途。** 为使用报表的用户标识报表的用途。 设计精良的报表提供的信息可为报表读者指引深层次情况和行动的方向。 在此阶段中所做的设计决策将影响您对报表参数、报表布局设计和报表查看体验的选择。 有关详细信息，请参阅[规划报表（报表生成器）](../../reporting-services/report-design/planning-a-report-report-builder.md)和[报表设计提示（报表生成器和 SSRS）](../../reporting-services/report-design/report-design-tips-report-builder-and-ssrs.md)。  
  
-   **选择查询的类型。** 确定是使用一般形式的共享数据集查询，还是使用特定于你的一组报表的数据集查询。 具有一般形式的查询的共享数据集易于维护以便多个报表使用，但每个报表设计者必须根据需要为其特定的报表组筛选数据。 有关详细信息，请参阅[报表数据 (SSRS)](../../reporting-services/report-data/report-data-ssrs.md)。  
  
-   **计划相关数据的视图。** 计划报表读者的查看体验。 能够深化到详细数据的汇总报表是用于处理大量数据的很有用的方法。 有关详细信息，请参阅 [钻取、深化、子报表和嵌套数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)。  
  
-   **配置权限。** 为授予正确的权限级别计划策略。 一个常见策略就是在报表服务器上创建文件夹结构，并且基于角色和文件夹安全性授予对报表和报表相关项的访问权限。 有关详细信息，请参阅 [保护报表](#bkmk_SecureReportsSummary)。  
  
-   **选择创作环境。** 不同的创作工具对功能的支持也有所不同。 有关详细信息，请参阅 [Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)。  
  
-   对于各报表：  
  
    -   **标识数据源。** 定义报表数据源，每个数据源一个定义。 有关详细信息，请参阅 [数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
  
    -   **从每个数据源选择要使用的数据。** 对于每个数据源，定义报表数据集。 每个数据集都包含指定要使用的数据的查询。 如果您具有报表参数，则定义数据集以便为每个参数填充可用值列表。 有关详细信息，请参阅[报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)[报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)。  
  
    -   **选择数据可视化。** 对于每个数据集，选择要用于显示数据的数据区域。 从表、图表、仪表和地图的列表中进行选择。 有关详细信息，请参阅以下主题：  
  
        -   [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
        -   [图表&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
        -   [迷你图和数据条（报表生成器和 SSRS）](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
        -   [指示器（报表生成器和 SSRS）](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
        -   [地图（报表生成器和 SSRS）](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)  
  
        -   [仪表（报表生成器和 SSRS）](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
    -   **自定义数据和布局。** 设计报表布局。 报表定义具有表体、数据源、数据集、数据区域、文本框、线条和图像。 矩形用作布局以及可视元素的容器。 通过撰写表达式以便控制对数据的筛选、分组、排序、格式设置和显示，对每个数据区域进行自定义。 添加报表名称、位置以及可帮助管理几十或数百个报表的其他标识信息。 添加可视元素和容器以便组织页面上的布局元素。 有关详细信息，请参阅以下主题：  
  
        -   [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
        -   [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
        -   [表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
        -   [设置报表项的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)  
  
        -   [图像、文本框、矩形和线条（报表生成器和 SSRS）](../../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md)  
  
        -   [页面布局和呈现方式（报表生成器和 SSRS）](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)  
  
    -   **配置交互功能。** 为你的报表访问者添加交互功能。 例如，添加排序按钮或切换项以便查看查询。 有关详细信息，请参阅[交互式排序、文档结构图和链接（报表生成器和 SSRS）](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)。  
  
    -   **查看和反复修改设计。** 预览报表。 发布一个初始版本，以便收集来自报表读者的反馈。 反复修改设计。  
  
-   **查看报表解决方案。** 验证报表组是否正确交互。  
  
-   **考虑可重复使用的组件。**  确定是否可共享任何数据源或数据集查询以便重复使用。 如果可共享，则在报表服务器或 SharePoint 站点上，创建共享数据源和共享数据集。 确定数据区域是否适合于重复作为报表部件使用。 有关详细详细信息，请参阅[报表设计器中的报表部件 (SSRS)](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)。  
  
## <a name="preview-reports"></a>预览报表  
 每种报表创作工具都支持预览报表。 有关详细信息，请参阅[使用报表设计器设计报表 (SSRS)](../../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md) 中的[预览](../../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_Preview)一节和[在报表生成器中预览报表](../../reporting-services/report-builder/previewing-reports-in-report-builder.md)。  
  
## <a name="save-or-publish-reports"></a>保存或发布报表  
 每种创作工具都支持在本地保存报表，或者支持将报表发布到报表服务器或 SharePoint 站点。 有关详细信息，请参阅[使用报表设计器设计报表 (SSRS)](../../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md) 中的[保存和部署](../../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_SaveandDeploy)一节和[保存报表（报表生成器）](../../reporting-services/report-builder/saving-reports-report-builder.md)。  
  
## <a name="view-reports"></a>查看报表  
 除了预览在本地保存的报表或发布到报表服务器的报表之外，您还可为报表读者提供多种查看体验。 查看报表：  
  
-   **浏览器。**  使用报表服务器 Web 服务或 SharePoint 站点查看已发布的报表。 在 SharePoint 站点上，您还可以配置 Web 部件以便查看已发布的报表。 有关详细信息，请参阅 [Reporting Services 和 Power View 的浏览器支持](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)、[报表管理器（SSRS 本机模式）](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)和 [URL 访问 (SSRS)](../../reporting-services/url-access-ssrs.md)。  
  
-   **传递。**  配置订阅以便以电子邮件的形式将报表传递给报表读者，或者传递到共享文件夹。  有关详细信息，请参阅[订阅和传递 (Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)。  
  
-   **导出。**  从报表查看器工具栏中，报表读者可以将报表导出为不同的文件格式。 导出文件格式可由报表服务器管理员配置。 有关详细信息，请参阅[导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
-   **打印。**  报表读者可根据查看报表的方式，打印报表或报表页。 有关详细信息，请参阅[打印报表（报表生成器和 SSRS）](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)。  
  
-   **Web 或 Windows 窗体应用程序。**  使用 Visual Studio 可以开发承载报表查看器控件的 ASP.NET AJAX 应用程序或 Windows 窗体应用程序。 该控件可以指向报表服务器上已发布的报表。 有关详细信息，请参阅 [Microsoft 报表](https://go.microsoft.com/fwlink/?LinkID=205399)。  
  
## <a name="manage-reports"></a>管理报表  
 管理已发布报表：  
  
-   **数据源。** 共享数据源和嵌入数据源都独立于报表定义进行管理。  
  
-   **数据集。**  共享数据集独立于报表定义进行管理。  
  
-   **参数。**  不通过报表定义单独管理参数。 在报表服务器上更改参数后，报表创作客户端将无法发布在服务器上进行的更改。  
  
-   **资源。**  ESRI 形状文件中的图像和空间数据是可以独立于报表定义而单独发布和管理的资源。  
  
-   **报表缓存。**  通过计划在非高峰期运行大型报表，可以降低业务峰值时段对报表服务器产生的处理影响。  
  
-   **快照。**  需要为必须使用相同数据集的多个用户提供一致结果时，可使用报表快照。 使用可变数据的按需运行报表每分钟都会生成不同的结果。 相反，报表快照则可用来针对包含同一时间点数据的其他报表或分析工具进行有效比较。  
  
-   **报表历史记录。** 通过创建一系列报表快照，您可以生成一个显示数据随时间变化情况的报表历史记录。  
  
 有关性能的详细信息，请参阅[性能、快照、缓存 (Reporting Services)](../../reporting-services/report-server/performance-snapshots-caching-reporting-services.md)。  
  
##  <a name="bkmk_SecureReportsSummary"></a> 保护报表  
 保护报表：  
  
-   从报表服务器管理员，标识用于您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装的授权和身份验证系统。 默认情况下， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用 Windows 身份验证、集成的安全性和角色分配来帮助控制对已发布报表的访问。 有关详细信息，请参阅[角色和权限 (Reporting Services)](../../reporting-services/security/roles-and-permissions-reporting-services.md) 和 [Reporting Services 安全性和保护](../../reporting-services/security/reporting-services-security-and-protection.md)。  
  
## <a name="create-notifications-based-on-report-data"></a>基于报表数据创建通知  
 您可以为 SharePoint 站点上的已发布报表创建数据警报。 数据警报基于报表的数据区域中的数据馈送。 默认情况下，将自动对数据区域进行命名。 报表作者可以通过基于其业务用途命名数据区域，更轻松地在其报表中创建数据区域。 在您创建数据警报时，如果数据满足您指定的条件，您将收到以电子邮件形式发出的通知。 有关详细信息，请参阅[基于报表生成数据馈送（报表生成器和 SSRS）](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)、[在数据警报设计器中创建数据警报](../../reporting-services/create-a-data-alert-in-data-alert-designer.md)和 [Reporting Services 数据警报](../../reporting-services/reporting-services-data-alerts.md)。  
  
## <a name="upgrade-reports"></a>Upgrade Reports  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支持报表定义、报表服务器和 SharePoint 站点的多个版本。 升级报表：  
  
-   升级报表服务器安装。 在首次使用时自动升级报表服务器上存储的已编译报表。 报表定义 (.rdl) 不更改。 有关详细信息，请参阅 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)。  
  
-   在报表创作环境中打开一个报表。 在大多数环境下将升级报表定义。 有关详细信息，请参阅[升级报表](../../reporting-services/install-windows/upgrade-reports.md)和 [SQL Server Data Tools 中的部署和版本支持 (SSRS)](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)。  
  
## <a name="troubleshoot-reports"></a>报表故障排除  
 报表故障排除：  
  
-   **确定出现问题的地方。** 查看 [报表阶段](#bkmk_StagesSummary)。  
  
-   **确定在哪里可以找到详细信息。** 例如，对于包含表达式的报表设计，与报表生成器工具相比，报表设计器工具提供与表达式计算问题有关的更详细信息。 对于报表处理错误，日志文件包含详细信息。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)   
 [扩展插件 (SSRS)](../../reporting-services/extensions-ssrs.md)   
 [Reporting Services 报表服务器](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)  
  
  
