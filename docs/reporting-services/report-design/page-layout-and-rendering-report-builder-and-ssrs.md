---
title: "页面布局和呈现 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e2358653-35bc-4496-810a-d3ccf02f229f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d688ed124a419017e97d405d7f5bd80e6e3bf530
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="page-layout-and-rendering-report-builder-and-ssrs"></a>页面布局和呈现方式（报表生成器和 SSRS）
阅读有关用于分页报表的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 呈现扩展插件的信息，以便可确定报表的外观按所需方式呈现，包括页面布局、分页符和纸张大小。 

 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器中或者报表生成器或报表设计器的预览窗格中查看报表时，报表首先由 HTML 呈现器呈现。 然后，可以将报表导出为不同格式，例如，Excel 或以逗号分隔 (CSV) 的文件。 接着，导出的报表可用于在 Excel 中进行进一步分析，或用作可以导入和使用 CSV 文件的应用程序的数据源。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含一组用于将报表导出为不同格式的呈现器。 每个呈现器在呈现报表时都需要应用规则。 当您将报表导出为其他文件格式时（尤其对于像 Adobe Acrobat (PDF) 呈现器这类根据实际页面大小进行分页的呈现器），您可能需要更改报表的布局，以便在应用呈现规则后，导出的报表能够正确地显示和打印。  
  
 对于导出的报表获得最佳结果通常是一个循环往复的过程：在报表生成器或报表设计器中创作和预览报表，将报表导出为首选的格式，检查导出的报表，然后对报表进行更改。  
    
##  <a name="PageLayout"></a> 报表项  
 报表项是与不同类型的报表数据关联的布局元素。 
 
* 表、矩阵、列表、图表和仪表都是分别链接到一个报表数据集的数据区域报表项。 处理报表时，数据区域会在报表页内横向和向下扩展，以便显示数据。 

其他报表项则链接到单个项并显示单个项。 
* **“图像”** 报表项可链接到图片。 
* **“文本框”** 报表项包含简单文本（如标题）或表达式（可以包含对内置字段、报表参数或数据集字段的引用）。 
* **“线条”** 和 **“矩形”** 报表项可向报表页提供简单图形元素。 **“矩形”** 还可以是其他报表项的容器。 

报表还可以包含子报表。  
  
## <a name="page-layout"></a>页面布局

 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，可以在设计图面的任意位置放置报表项。 可以使用对齐线和尺寸调整控点以交互方式定位、扩展和指定报表项的初始形状。 您可以并行放置具有不同数据集的数据区域，甚至是具有不同格式的同一数据的数据区域。 在设计图面上放置报表项时，报表项便会具有默认的大小、形状以及与所有其他报表项的初始关系。 
 
 可以将报表项放置在其他报表项内，以便创建更复杂的报表设计。 例如，图表或图像位于表单元中、表位于表单元中并且多个图像位于一个矩形中。 除了提供您在报表中所需的组织形式和外观外，将报表项置于矩形之类的容器中还帮助您控制报表项在报表页上显示的方式。  
  
 报表可以跨越多个页，每个页上都可以有重复的页眉和页脚。 报表可包含图形元素，如图像和线条，并可具有多种基于表达式的字体、颜色和样式。  
  
##  <a name="ReportSections"></a> 报表区域  
 报表由三个主要区域组成：页眉（可选）、页脚（可选）和表体。 报表的页眉和页脚不是独立的报表区域，而是由放置在表体的顶部和底部的报表项组成。 页眉和页脚会在报表每一页的顶部和底部重复相同的内容。 您可以在页眉和页脚中放置图像、文本框和线条。 可以在表体中放置任何类型的报表项。  
  
 您可以设置报表项的属性，以便一开始就在页中隐藏或显示该报表项。 可以设置数据区域的行、列或组的可见性属性，并提供切换按钮使用户能以交互方式显示或隐藏报表数据。 还可以使用表达式（包括基于报表参数的表达式）来设置可见性或初始可见性。  
  
 处理报表时，会将报表数据与报表布局元素组合起来，并将组合的数据发送到报表呈现器。 呈现器会根据报表项扩展插件的预定义规则，确定每一页能够容纳的数据量。 若要设计对您要使用的呈现器而言最优的易读报表，您需要了解 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中用于控制分页的规则。 有关详细信息，请参阅 [Reporting Services 中的分页（报表生成器和 SSRS）](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)。  
  
##  <a name="RenderingExtensions"></a> 呈现器  
 Reporting Services 包括一组呈现器，也称为呈现扩展插件，可用来将报表导出为其他格式。 有三种类型的呈现器：  
  
-   **数据呈现器** ：数据呈现器会去除报表中的所有格式设置和布局信息而仅显示数据。 可使用所产生的文件将原始报表数据导入为其他文件类型，如 Excel、其他数据库、XML 数据消息或自定义应用程序。 可用的数据呈现器为 CSV 和 XML。  
  
    > [!NOTE]  
    >  尽管它没有提供直接导出到其他格式的功能，但 Atom 呈现从报表中生成数据文件。  
  
-   **软分页呈现器** ：软分页呈现器保留报表的布局和格式设置。 对所产生的文件进行优化，以便满足基于屏幕的查看和传递（例如在网页上）的需要。 可用的软分页呈现器有： [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word、Web 存档 (MHTML) 和 HTML。  
  
-   **硬分页呈现器** ：硬分页呈现器保留报表的布局和格式设置。 对所产生的文件进行了优化，以便提供一致的打印体验或以书本格式联机查看报表。 可用硬分页呈现器：TIFF 和 PDF。  
  
 在报表生成器或报表设计器中预览报表时，或者在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器中运行报表时，报表总是首先以 HTML 格式呈现。 在运行报表后，您可以将其导出为不同的文件格式。 有关详细信息，请参阅 [导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)中用于控制分页的规则。  
  
##  <a name="RenderingBehaviors"></a> 呈现行为  
 根据选择的呈现器，当呈现报表时，将应用特定的规则。 报表项在页面上的呈现方式由以下因素综合确定：  
  
-   呈现规则。  
-   报表项的高度和宽度。  
-   表体的大小。  
-   页面的高度和宽度。  
-   特定于呈现器的分页支持。  
  
 例如，呈现为 HTML 和 MHTML 格式的报表针对基于计算机屏幕的体验进行了优化，其中的页面可以是各种长度。  
  
 有关详细信息，请参阅[呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
   
##  <a name="Pagination"></a> 分页  
 分页方式指的是报表内的页数以及报表项在这些页上的排列方式。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的分页方式因您用来查看和传递报表的呈现扩展插件以及您配置报表使用的分页符和哪些项目放在同一页的选项不同而异。  
  
 若要成功设计一个对用户而言易于阅读、对准备用于传递报表的呈现器而言最优的报表，需要了解在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中用于控制分页的规则。 使用 **数据** 和 **软分页** 呈现扩展插件导出的报表通常不受分页影响。 当您使用数据呈现扩展插件时，报表将呈现为 XML 或 CSV 格式的表格行集。 为了确保导出的报表数据有用，应了解所应用的规则从报表呈现了一个平展的表格行集。  
  
 使用 **软分页** 呈现扩展插件（如 HTML 呈现扩展插件）时，可能想知道报表打印后的外观以及使用硬分页呈现器（如 PDF）呈现此报表时可以达到哪种理想效果。 在创建或更新报表时，您可以在报表生成器和报表设计器中预览和导出此报表。  
  
 **硬分页**呈现器对于报表布局和实际页面大小的影响最大。 若要了解详细信息，请参阅 [Reporting Services 中的分页（报表生成器和 SSRS）](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)。  
   
##  <a name="HowTo"></a> 操作指南主题  
 本节列出的过程分步向您介绍如何在报表中使用分页。  
  
-   [添加分页符（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md)  
  
-   [在多个页中显示行标题和列标题（报表生成器和 SSRS）](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)  
  
-   [添加或删除页面页眉或页脚（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)  
  
-   [在滚动报表时保持标题可见（报表生成器和 SSRS）](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
-   [显示页码或其他报表属性（报表生成器和 SSRS）](../../reporting-services/report-design/display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md)  
  
-   [隐藏第一页或最后一页的页眉或页脚（报表生成器和 SSRS）](../../reporting-services/report-design/hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md)  
  
##  <a name="InThisSection"></a> 本节内容  
 以下主题介绍有关页面布局和呈现方式的其他信息：  
  
 [页眉和页脚（报表生成器和 SSRS）](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)  
 提供有关如何在报表中使用页眉和页脚以及如何使用它们来控制分页的信息。  
  
 [控制分页符、标题、列和行（报表生成器和 SSRS）](../../reporting-services/report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)  
 提供有关使用分页符的信息。  
  
## <a name="see-also"></a>另请参阅  
 [不同报表呈现扩展插件的交互功能（报表生成器和 SSRS）](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
