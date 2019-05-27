---
title: 导出报表 （报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10437"
ms.assetid: a2bab8c1-505d-4da3-b1db-ea0ae13b2336
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d8b4fe6e791f84f0949b0657b890c79db99dfbf9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107949"
---
# <a name="exporting-reports-report-builder-and-ssrs"></a>导出报表（报表生成器和 SSRS）
  运行报表后，可以将其导出为其他格式（如 Excel 或 PDF），也可以通过生成 Atom 服务文档，列出可从报表获得的与 Atom 兼容的数据馈送来导出报表。  
  
 导出报表后，可以执行以下操作：  
  
-   在其他应用程序中处理报表数据。 例如，可以将报表导出为 Excel 格式，然后在 Excel 中继续处理相应数据。  
  
-   以不同的格式打印报表。 例如，可以将报表导出为 PDF 文件格式，并打印报表。  
  
-   将报表的副本另存为其他文件类型。 例如，可以将报表导出为 Word 格式并将其保存来创建报表的副本。  
  
-   在应用程序中将报表数据用作数据馈送。 例如，可以生成 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 客户端可使用的与 Atom 兼容的数据馈送，然后在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]中处理数据。  
  
 报表管理器的报表查看器工具栏中提供了导出选项，当您查看报表服务器上的报表时或通过报表生成器的功能区预览报表时，每个报表的顶部会显示此工具栏。 此数据馈送选项仅在报表管理器中可用。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供多个呈现扩展插件，以支持将报表导出为常见文件格式。 呈现扩展插件支持带软分页的文件格式（如 Word 或 Excel）、带硬分页的文件格式（如 PDF 或 TIFF）或仅带数据的文件格式（如 CSV 或与 Atom 兼容的 XML）。  
  
 若要快速开始使用导出报表并从报表生成 Atom 兼容的数据馈送，请参阅[将报表导出为其他文件类型&#40;报表生成器和 SSRS&#41; ](../export-a-report-as-another-file-type-report-builder-and-ssrs.md)并[从生成数据馈送报表&#40;报表生成器和 SSRS&#41;](generate-data-feeds-from-a-report-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RendererTypes"></a> 呈现扩展插件类型  
 有三种类型的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 呈现扩展插件：  
  
-   **数据呈现扩展插件** 数据呈现扩展插件会去除报表中的所有格式设置和布局信息而仅显示数据。 可使用所产生的文件将原始报表数据导入为其他文件类型，如 Excel、其他数据库、XML 数据消息或自定义应用程序。 数据呈现器不支持分页。  
  
     支持以下数据呈现扩展插件：CSV、 XML 和 Atom。  
  
-   **软分页呈现扩展插件** 软分页呈现扩展插件保留报表的布局和格式设置。 为了满足基于屏幕的查看和传递（例如在网页上或在 **ReportViewer** 控件中）需要，对所产生的文件进行优化。  
  
     支持以下软分页呈现扩展插件：[!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 和 Web 存档 (MHTML)。  
  
-   **硬分页呈现扩展插件** 硬分页呈现扩展插件保留报表的布局和格式设置。 对所产生的文件进行了优化，以便提供一致的打印体验或以书本格式联机查看报表。  
  
     支持以下硬分页呈现扩展插件：TIFF 和 PDF。  
  
##  <a name="ExportFormats"></a> 导出格式  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了用于以不同格式呈现报表的呈现扩展插件。 如果您打算使用此功能，则应当针对您所选的文件格式优化报表设计。 有关每个呈现扩展插件的主题提供了有关如何以相应格式呈现报表的详细信息。  
  
 下表列出了可用的格式。  
  
|格式|呈现扩展插件类型|Description|  
|------------|------------------------------|-----------------|  
|CSV|数据|逗号分隔值 (CSV) 呈现扩展插件以平展的表示形式呈现报表中的数据，格式为标准化的纯文本，这种数据表示形式容易读取且可与多个应用程序交换。<br /><br /> 有关详细信息，请参阅 [导出到 CSV 文件（报表生成器和 SSRS）](exporting-to-a-csv-file-report-builder-and-ssrs.md)中处理数据。|  
|“导出”|软分页|如果安装了针对 Word、Excel 和 PowerPoint 的 Microsoft Office 兼容包，Excel 呈现扩展插件可将报表呈现为能够兼容 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007-2010 及 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 的 Excel 文档。 将报表导出至 Excel 工作表时，将会去掉一些布局和原始设计元素。可以设置报表属性和报表内的组以便在将报表导出到 Excel 时启用工作表选项卡的命名。 此呈现器生成的文件的文件扩展名为 xlsx。<br /><br /> 有关详细信息，请参阅 [导出到 Microsoft Excel（报表生成器和 SSRS）](exporting-to-microsoft-excel-report-builder-and-ssrs.md)中处理数据。<br /><br /> 注意：Excel 2003 呈现扩展插件呈现的本机格式为[!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)]2003年是在某些报告方案中。|  
|Word|软分页|如果安装了针对 Word、Excel 和 PowerPoint 的 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] Office 兼容包，Word 呈现扩展插件可将报表呈现为能够兼容 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010 及 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 2003 的 Word 文档。 报表导出为 Word 文档后，可以更改报表内容并设计文档样式的报表，例如邮件标签、采购订单或套用信函。 此呈现器生成的文件的文件扩展名为 docx。<br /><br /> 有关详细信息，请参阅 [导出到 Microsoft Word（报表生成器和 SSRS）](exporting-to-microsoft-word-report-builder-and-ssrs.md)中处理数据。<br /><br /> 注意：Word 2003 呈现扩展插件呈现的本机格式为[!INCLUDE[ofprword](../../includes/ofprword-md.md)]2003年是在某些报告方案中。|  
|Web 存档|软分页|HTML 呈现扩展插件以 HTML 格式呈现报表。 该呈现扩展插件还可以生成完整的 HTML 页面，或生成 HTML 片段以嵌入其他 HTML 页面。 所有 HTML 都是使用 UTF-8 编码生成的。<br /><br /> 对于在报表生成器中预览并在浏览器中查看的报表（包括在报表管理器中运行时），HTML 呈现扩展插件都是默认的呈现扩展插件。<br /><br /> 有关详细信息，请参阅 [以 HTML 格式呈现（报表生成器和 SSRS）](rendering-to-html-report-builder-and-ssrs.md)中处理数据。|  
|Acrobat (PDF) 文件|硬分页|PDF 呈现扩展插件可将报表呈现为特定格式的文件，以便在 Adobe Acrobat 和其他支持 PDF 1.3 的第三方 PDF 查看器中打开。 尽管 PDF 1.3 与 Adobe Acrobat 4.0 及更高版本兼容，但 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支持 Adobe Acrobat 6 或更高版本。 呈现扩展插件不需要使用 Adobe 软件呈现报表。 不过，该插件需要使用 PDF 查看器（例如 Adobe Acrobat）才可查看或打印 PDF 格式的报表。<br /><br /> 有关详细信息，请参阅 [导出到 PDF 文件（报表生成器和 SSRS）](exporting-to-a-pdf-file-report-builder-and-ssrs.md)中处理数据。|  
|TIFF 文件|硬分页|图像呈现扩展插件可以将报表呈现为位图或图元文件。 默认情况下，图像呈现扩展插件将生成报表的 TIFF 文件，您可以按多页形式查看此类文件。 客户端收到图像时，可以在图像查看器中显示图像，并可以打印图像。<br /><br /> 图像呈现扩展插件可以在任何支持的格式生成文件[!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]:BMP、 EMF、 EMFPlus、 GIF、 JPEG、 PNG 和 TIFF。<br /><br /> 有关详细信息，请参阅 [导出到图像文件（报表生成器和 SSRS）](exporting-to-an-image-file-report-builder-and-ssrs.md)中处理数据。|  
|XML|数据|XML 呈现扩展插件可以按 XML 格式返回报表。 报表 XML 的架构专用于相应的报表，并且只包含数据。 布局信息呈现以及分页都不是由 XML 呈现扩展插件完成。 此扩展插件生成的 XML 可以导入到数据库中用作 XML 数据消息，或发送到自定义应用程序。<br /><br /> 有关详细信息，请参阅 [导出到 XML（报表生成器和 SSRS）](exporting-to-xml-report-builder-and-ssrs.md)中处理数据。|  
|Atom|数据|Atom 呈现扩展插件将从报表生成与 Atom 兼容的数据馈送。 数据馈送是可读的，并可以与可使用与 Atom 兼容的数据馈送的应用程序（如 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 客户端）进行交换。<br /><br /> 输出为一个 Atom 服务文档，该文档列出报表中可用的数据馈送。 为报表中的每个数据区域至少创建一个数据馈送。 根据数据区域的类型以及数据区域显示的数据，可以生成多个数据馈送。<br /><br /> 有关详细信息，请参阅 [基于报表生成数据馈送（报表生成器和 SSRS）](generating-data-feeds-from-reports-report-builder-and-ssrs.md)中处理数据。|  
  
##  <a name="ExportingReport"></a> 导出报表  
 若要导出某个报表，请在报表管理器或报表生成器中运行该报表，然后从“导出”下拉列表中选择一种格式。 系统会提示您选择保存还是打开文件。 如果您选择 **“打开”**，将根据您选择的呈现格式在关联的应用程序中打开该报表。 （例如，当您选择 **Excel** 时，该报表便会在 Excel 中打开）。 如果您选择 **“保存”**，则保存该报表。 例如，如果导出到 Excel，则将报表保存为 .xls 文件。 为本地计算机定义的文件关联确定对于特定的呈现格式将使用哪一个应用程序。 有关详细信息，请参阅[将报表导出为其他文件类型&#40;报表生成器和 SSRS&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md)。  
  
 报表服务器按报表在当前用户会话中的原样导出报表。 如果在您打开报表时或报表显示的数据发生更改时，有人发布了该报表的更新版本，则不会更新已导出的报表。  
  
 当以不同的格式导出报表时，报表分页可能会受到影响。 预览报表时，您查看的是遵循软分页规则的 HTML 呈现扩展插件呈现的报表效果。 将报表导出为其他文件格式（如 Adobe Acrobat (PDF)）时，分页是根据物理页大小进行的，这遵循的是硬分页规则。 还可以用您添加到报表的逻辑分页符来分隔各页，但页的实际长度会因您使用的呈现器类型而异。 若要更改报表的分页情况，必须了解您选择的呈现扩展插件的分页行为。 您可能需要针对此呈现扩展插件调整报表布局的设计。 有关详细信息，请参阅[页面布局和呈现方式（报表生成器和 SSRS）](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md)。  
  
##  <a name="GeneratingDataFeedsFromReport"></a> 从报表生成数据馈送  
 若要从某个报表生成数据馈送，请在报表管理器中运行该报表，然后单击报表管理器工具栏上的 **“生成数据馈送”** 图标。 系统会提示您选择保存还是打开文件。 如果您选择 **“打开”**，则将在应用程序中打开与 .atomsvc 文件扩展名关联的 Atom 服务文档。 如果您选择 **“保存”**，则将该文档另存为 .atomsvc 文件。 默认情况下，该文件的名称即为报表的名称。 您可以将此名称更改为一个更有意义的名称。  
  
 将该 Atom 服务文档保存到计算机上。 稍后，您可以将其上载到报表服务器或另一个服务器上以供他人使用。 有关详细信息，请参阅[基于报表生成数据馈送（报表生成器和 SSRS）](generating-data-feeds-from-reports-report-builder-and-ssrs.md)和[从报表生成数据馈送（报表生成器和 SSRS）](generate-data-feeds-from-a-report-report-builder-and-ssrs.md)。  
  
##  <a name="Troubleshooting"></a> 排除与导出的报表有关的问题  
 有时候，在您将报表导出到不同格式后，它们看起来不同或者没有按您预期的方式工作。 出现此问题的原因是某些规则和限制可能应用于呈现器。 在创建报表时，可以考虑这些来解决许多限制。 在报表中可能需要使用稍有不同的布局，仔细对齐报表中的项，将报表表尾限制为单行文本等。  
  
 如果报表包含带有阿拉伯数字的 Unicode 文本，或包含以阿拉伯数字表示的日期，当你将报表导出为以下任何一种格式或打印报表时，这些日期和数字将不会正确呈现。  
  
-   PDF  
  
-   Word  
  
-   “导出”  
  
-   图像/TIFF  
  
 如果将报表导出为 HTML，日期和数字将正确呈现。  
  
 与特定呈现器有关的主题介绍报表项和数据区域是如何呈现的以及对于每种呈现器的限制和解决方法。  
  
-   [导出到 CSV 文件（报表生成器和 SSRS）](exporting-to-a-csv-file-report-builder-and-ssrs.md)  
  
-   [导出到 Microsoft Excel（报表生成器和 SSRS）](exporting-to-microsoft-excel-report-builder-and-ssrs.md)  
  
-   [导出到 Microsoft Word（报表生成器和 SSRS）](exporting-to-microsoft-word-report-builder-and-ssrs.md)  
  
-   [以 HTML 格式呈现（报表生成器和 SSRS）](rendering-to-html-report-builder-and-ssrs.md)  
  
-   [导出到 PDF 文件（报表生成器和 SSRS）](exporting-to-a-pdf-file-report-builder-and-ssrs.md)  
  
-   [导出到图像文件（报表生成器和 SSRS）](exporting-to-an-image-file-report-builder-and-ssrs.md)  
  
-   [导出到 XML（报表生成器和 SSRS）](exporting-to-xml-report-builder-and-ssrs.md)  
  
-   [基于报表生成数据馈送（报表生成器和 SSRS）](generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供附加的功能来帮助您创建采用其他格式可以很好地工作的报表。 Tablix 数据区域（表、矩阵和列表）、组和矩形上的分页符使您可以更好地控制报表分页。 由分页符分隔的报表页可以具有不同的页名称和重置页码编号。 通过使用表达式，可以在报表运行时动态更新页名称和页码。 有关详细信息，请参阅 [Reporting Services 中的分页（报表生成器和 SSRS）](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)。  
  
 此外，您还可以使用 RenderFormat 内置全局属性，针对不同呈现器有条件地应用不同的报表布局。 有关详细信息，请参阅[内置的全局和用户引用（报表生成器和 SSRS）](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)。  
  
##  <a name="OtherWaysExportingReports"></a> 导出报表的其他方式  
 导出报表是在报表管理器或报表生成器中打开报表时可以根据需要执行的一项任务。 若要自动执行导出操作（例如，根据重复执行的计划，将报表以特定文件类型导出到共享文件夹中），请创建一个订阅，将报表传递到共享文件夹。 有关详细信息，请参阅 [File Share Delivery in Reporting Services](../subscriptions/file-share-delivery-in-reporting-services.md)。  
  
 在报告工具中预览或在浏览器应用程序（如报表管理器）中打开的报表始终首先以 HTML 格式呈现。 不能将其他呈现扩展插件指定为用于查看的默认扩展插件。 但是，可以创建一个订阅，使用该订阅按所需呈现格式生成报表，然后再传递到电子邮件收件箱或共享文件夹。 有关详细信息，请参阅[创建、 修改和删除标准订阅&#40;本机模式下的 Reporting Services&#41; ](../subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)并[创建、 修改和删除数据驱动订阅](../subscriptions/data-driven-subscriptions.md)。  
  
 您也可以通过将呈现扩展插件指定为 URL 参数的 URL 来访问报表，并直接将报表呈现为指定格式，而不先将报表呈现为 HTML 格式。 下面的示例将报表呈现为 Excel 格式：  
  
```  
http://<Server Name>/reportserver?/Sales/YearlySalesSummary&rs:Format=Excel&rs:Command=Render  
```  
  
 有关详细信息，请参阅 [Export a Report Using URL Access](../export-a-report-using-url-access.md)。  
  
## <a name="see-also"></a>请参阅  
 [控制分页符、标题、列和行（报表生成器和 SSRS）](../report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [查找、查看和管理报表（报表生成器和 SSRS）](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [打印报表（报表生成器和 SSRS）](print-reports-report-builder-and-ssrs.md)   
 [保存报表（报表生成器）](saving-reports-report-builder.md)  
  
  
