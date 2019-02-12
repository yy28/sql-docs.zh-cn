---
title: Reporting Services 中的分页（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e0894b0d-dc5b-4a75-8142-75092972a034
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bf2f253405e3e64764f3b7edf61112a3bb05d601
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025078"
---
# <a name="pagination-in-reporting-services-report-builder--and-ssrs"></a>Reporting Services 中的分页（报表生成器和 SSRS）
  分页方式指的是报表内的页数以及报表项在这些页上的排列方式。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的分页方式因您用来查看和传递报表的呈现扩展插件而异。 在报表服务器上运行报表时，相应报表使用的是 HTML 呈现器。 HTML 遵循一组特定的分页规则。 如果将同一报表导出为其他格式，例如 PDF，系统会使用 PDF 呈现器并应用另一组规则；因此，该报表的分页方式就会不同。 若要成功设计一个对用户而言易于阅读、对准备用于传递报表的呈现器而言最优的报表，需要了解在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]中用于控制分页的规则。  
  
 本主题讨论了物理页大小和报表布局对硬分页符呈现器呈现报表的方式有何影响。 您可以使用 **“报表属性”** 窗格、 **“属性”** 窗格或 **“页面设置”** 对话框来设置属性，以修改物理页大小和边距，以及将报表分为多个列。 您可通过单击报表正文外面的蓝色区域来访问 **“报表属性”** 窗格。 通过单击“主文件夹”选项卡上的 **“运行”** 然后再单击“运行”选项卡上的 **“页面设置”** ，可以访问 **“页面设置”** 对话框。  
  
> [!NOTE]  
>  如果您已将报表宽度设计为一页，但该报表却跨多页呈现，请检查表体的宽度（包括边距）是否不超过物理页大小宽度。 若要防止向报表中添加空页，可以通过将容器角向左拖动来减小容器大小。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="the-report-body"></a>表体  
 表体是在设计图面上显示为空白的矩形容器。 该容器可以扩大或收缩以容纳其中包含的报表项。 表体不反映物理页大小，实际上表体的大小可以增大至超过物理页大小的界限，乃至跨越多个报表页。 有些呈现器（比如 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)]、Word、HTML 和 MHTML）可呈现根据页面内容进行扩大或收缩的报表。 以这些格式呈现的报表针对基于屏幕的查看方式（例如在 Web 浏览器中查看）进行了优化。 如果需要，这些呈现器会添加垂直分页符。  
  
 您可以设置表体的格式，使其具有边框颜色、边框样式和边框宽度。 还可以添加背景色和背景图像。  
  
## <a name="the-physical-page"></a>物理页  
 物理页大小为纸张大小。 您为报表指定的纸张大小控制着报表的呈现方式。 以硬分页符格式呈现的报表会根据物理页大小在水平方向和垂直方向上插入分页符，以便在以硬分页符文件格式打印或查看时提供最佳的阅读体验。 以软分页符格式呈现的报表会根据物理页大小在水平方向上插入分页符，以便在 Web 浏览器中查看时提供最佳的阅读体验。  
  
 默认情况下，页面大小为 8.5 x 11 英寸，但可以通过以下方式更改此大小：使用“报表属性”窗格、“页面设置”对话框，或在“属性”窗格中更改 PageHeight 和 PageWidth 属性。 页大小不会扩大或收缩以容纳表体的内容。 如果希望报表显示在单个页上，则物理页上必须能够容纳表体中的所有内容。 如果无法容纳并且您使用的是硬分页符格式，则报表将需要占用其他页。 如果表体因扩大而超过了物理页的右边缘，则会在水平方向上插入一个分页符。 如果表体因扩大而超过了物理页的下边缘，则会在垂直方向上插入一个分页符。  
  
 如果要覆盖报表中定义的物理页大小，可以使用您用来导出报表的特定呈现器的“设备信息”设置来指定物理页大小。 有关详细信息，请参阅 [Reporting Services Device Information Settings](https://go.microsoft.com/fwlink/?LinkId=102515)（Reporting Services 设备信息设置）。  
  
### <a name="margins"></a>边距  
 边距从物理页大小的边缘开始向内绘制到指定的边距设置。 如果一个报表项延伸至边距区域内，则会裁剪该项以便不呈现重叠区域。 如果您指定的边距大小导致页的水平宽度或垂直宽度等于零，则边距设置默认为零。 可通过以下方法指定边距：使用“报表属性”窗格、“页面设置”对话框，或在“属性”窗格中更改 TopMargin、BottomMargin、LeftMargin 和 RightMargin 属性。 如果要覆盖报表中定义的边距大小，可以使用您用来导出报表的特定呈现器的“设备信息”设置来指定边距大小。  
  
 为边距、列间距、页眉和页脚分配空间后剩下的物理页区域称为“可用页区域” 。 只有在您以硬分页符呈现器格式呈现和打印报表时才会应用边距。 下图指示了一个物理页的边距和可用页区域。  
  
 ![带有边距和可用区域的物理页。](../media/rspagemargins.gif "带有边距和可用区域的物理页。")  
  
### <a name="newsletter-style-columns"></a>新闻稿样式列  
 报表可分成多列（就像报纸中的各栏一样），这些列被视为在同一物理页上呈现的逻辑页。 这些列按从左到右、从上到下的方式排列，各列之间以空白隔开。 如果报表分成多个列，则每个物理页被垂直划分为多个列，每列被视为一个逻辑页。 例如，假定在一个物理页上有两列。 报表内容将首先填充第一列，然后填充第二列。 如果在前两列中不能完全容纳此报表，则此报表会依次填充下一页上的第一列和第二列。 将按从左到右、从上到下的顺序继续填充列，直到呈现完所有报表项为止。 如果您指定的列大小导致水平宽度或垂直宽度等于零，则列间距默认为零。  
  
 可通过以下方法指定列：使用“报表属性”窗格、“页面设置”对话框，或在“属性”窗格中更改 TopMargin、BottomMargin、LeftMargin 和 RightMargin 属性。 如果要使用未定义的边距大小，可以使用您用来导出报表的特定呈现器的“设备信息”设置来指定边距大小。 只有在以 PDF 或图像格式呈现和打印报表时才会应用列。 下图指示了一个包含多个列的页的可用页区域。  
  
 ![带有所述列的物理页。](../media/rspagecolumns.gif "带有所述列的物理页。")  
  
## <a name="page-breaks-and-page-names"></a>分页符和页名称  
 当一个报表具有页名称时，该报表可能更具可读性并且其数据更易于审核和导出。 Reporting Services 为报表和 tablix 数据区域（表、矩阵和列表）、组和报表中的矩形提供属性，以便控制分页、重置页码和在分页符上提供新的报表页名称。 这些功能可以增强报表的效果，而与呈现报表的格式无关，但在将报表导出到 Excel 工作簿时特别有用。  
  
 InitialPageName 属性提供报表的初始页名称。 如果您的报表对于分页符不包括页名称，则初始页名称将用于由分页符创建的所有新页。 不需要使用初始页名称。  
  
 呈现的报表可为分页符导致的新页提供新的页名称。 为了提供页名称，可以设置表、矩阵、列表、组或矩形的 PageName 属性。 不需要对分页指定页名称。 如没有这样做，则改用 InitialPageName 的值。 如果 InitialPageName 也为空，则新页将没有名称。  
  
 Tablix 数据区域（表、矩阵和列表）、组和矩形支持分页符。  
  
 分页符包括以下属性：  
  
-   BreakLocation 为支持分页符的报表元素提供分页的位置：在开头、末尾或者开头和末尾。 在组上，BreakLocation 可位于两个组之间。  
  
-   Disabled 指示分页符是否应用于报表元素。 如果此属性的求值结果为 True，则忽略分页符。 此属性用于在报表运行时基于表达式动态地禁用分页符。  
  
-   ResetPageNumber 指示在出现分页符是否应将页码重置为 1。 如果此属性的求值结果为 True，则重置页码。  
  
 可以在“Tablix 属性”、“矩形属性”或“组属性”对话框中设置 BreakLocation 属性，但必须在报表生成器的“属性”窗格中设置 Disabled、ResetPageNumber 和 PageName 属性。 如果“属性”窗格中的属性按类别进行组织，则您将在 **PageBreak** 类别中找到这些属性。 对于组， **PageBreak** 类别位于 **“组”** 类别内。  
  
 可以使用常量以及简单或复杂表达式来设置 Disabled 和 ResetPageNumber 属性的值。 但是，不能将表达式用于 BreakLocation 属性。 有关编写和使用表达式的详细信息，请参阅[表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)。  
  
 在报表中，可以撰写通过使用 `Globals` 集合引用当前页名称或页码的表达式。 有关详细信息，请参阅[内置的全局和用户引用（报表生成器和 SSRS）](built-in-collections-built-in-globals-and-users-references-report-builder.md)。  
  
### <a name="naming-excel-worksheet-tabs"></a>命名 Excel 工作表选项卡  
 当您将报表导出到 Excel 工作簿时，以下属性非常有用。 使用 InitialPage 属性可以指定导出报表时工作表选项卡的默认名称，使用分页符和 PageName 属性可为每个工作表提供不同的名称。 分页符定义的每个新报表页将导出到由 PageName 属性的值命名的不同工作表中。 如果 PageName 为空白，但报表有一个初始页名称，则 Excel 工作簿中的所有工作表都将使用相同的名称，即该初始页名称。  
  
 有关在报表导出到 Excel 时这些属性的工作方式的详细信息，请参阅[导出到 Microsoft Excel（报表生成器和 SSRS）](../report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [页面布局和呈现方式（报表生成器和 SSRS）](page-layout-and-rendering-report-builder-and-ssrs.md)  
  
  
