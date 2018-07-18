---
title: 呈现行为（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8f873ef9-27a3-40e5-b58b-6774f8027a58
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4ddec1ab7e8252ff65beb241cfd71602fbe00465
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33027514"
---
# <a name="rendering-behaviors-report-builder--and-ssrs"></a>呈现行为（报表生成器和 SSRS）
  根据选择的呈现器，呈现报表时，将针对表体及其内容应用特定的规则。 报表项在页面上的呈现方式由以下因素综合确定：  
  
-   呈现规则。  
  
-   报表项的高度和宽度。  
  
-   表体的大小。  
  
-   页面的高度和宽度。  
  
-   特定于呈现器的分页支持。  
  
 本主题讨论 Reporting Services 所应用的一般规则。 有关详细信息，请参阅[呈现报表项（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)、[呈现数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-data-regions-report-builder-and-ssrs.md)和[呈现数据（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-data-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="general-behaviors-for-html-mhtml-word-and-excel-soft-page-break-renderers"></a>HTML、MHTML、Word 和 Excel（软分页呈现器）的一般行为  
 使用 HTML 和 MHTML 格式导出的报表针对基于计算机屏幕的体验进行了优化，其中的页面可以是各种长度。 仅在表体内的近似位置垂直插入分页符。 这些近似位置由“属性”窗格中的交互高度设置来确定。 例如，假定交互高度设置为 5 英寸。 呈现报表时，页面高度大约为 5 英寸长。 Word 和 Excel 基于逻辑分页符进行分页，并且忽略交互高度设置。  
  
> [!NOTE]  
>  若要确定报表如何在软分页呈现器中显示，请使用报表预览。 报表的显示方式与在 HTML、MHTML、Word 或 Excel 格式中的显示方式相同。  
  
 将报表导出到 HTML、MHTML、Word 或 Excel 时，应遵循下述一般规则：  
  
-   逻辑分页符（显式插入的分页符）应用于报表项。 例如，如果在每个组之间插入一个分页符，则在呈现报表时将应用这些分页符。  
  
-   通过使用页面高度和报表项显示的次数，可创建一个近似布局。 例如，如果文本框的高度为 0.5 英寸并在报表中重复 5 次，则会保留 2.5 英寸。  
  
-   根据交互高度的设置，可以插入多个软分页符。 若要在 HTML 和 ReportViewer 控件中取消软分页符，并仅使用显式分页符控制分页，请将 **interactive height** 值设置为 0 或一个极大的数。  
  
    > [!NOTE]  
    >  交互宽度设置不用于软分页呈现器。  
  
-   报表页可以增大以容纳需要显示在一起的末行、孤立行和报表项。 也就是说，报表可以扩展到屏幕宽度之外，并可使用滑动条来查看。  
  
-   分页仅垂直应用于报表。  
  
-   不应用页边距。  
  
## <a name="general-behaviors-for-pdf-image-and-print-hard-page-break-renderers"></a>PDF、图像和打印（硬分页呈现器）的一般行为  
 使用 PDF 和图像导出的报表针对书状或打印体验进行了优化，其中的页面大小保持一致。 在表体内的特定位置垂直和水平插入分页符。 这些特定位置由页面宽度和页面高度设置来确定。  
  
> [!NOTE]  
>  若要确定报表如何在硬分页呈现器中显示，请使用打印预览。 报表的显示方式与在 PDF 或图像格式中的显示方式相同。  
  
-   页的编号顺序是从左到右，然后再从上到下。  
  
-   逻辑分页符（显式插入的分页符）应用于报表项。 这些分页符会导致报表项将其他项推到下一页。  
  
-   如果物理分页符出现在必须显示在一起的报表项中，则必须显示在一起的项将移至下一页。  
  
-   由于页面大小的约束，可能无法将所有项显示在一起或重复项。 如果发生这种情况，呈现器可能忽略重复另一项的某些规则，以便允许报表项适合页面。  
  
-   如果项无法显示在一起（例如文本框太大无法适合垂直的可用页面区域），则该项将在物理页边界处剪掉并继续显示在下一页中。  
  
-   分页可垂直和水平应用于报表。  
  
    > [!NOTE]  
    >  交互宽度设置不用于硬分页呈现器。  
  
## <a name="minimum-spacing-between-report-items"></a>报表项间的最小间距  
 报表项可以在表体内增大以容纳其内容。 例如，呈现报表时，矩阵数据区域通常在页面内向下扩展，并且文本框的高度可随表达式返回的数据进行调整。  
  
 呈现器会在报表项间保留一个最小的间距，该间距在报表布局中定义。 在报表布局上将报表项相邻放置时，报表项间的距离在报表水平或垂直增长时将变成必须保持的最小距离。 例如，如果您向报表添加一个矩阵数据区域，然后在矩阵的右侧 0.25 英寸处添加一个矩形，则在矩阵增长时将保持最小间距。 每个项向右移动以便与其左侧的项之间保持最小距离。  
  
## <a name="page-headers-and-footers"></a>页眉和页脚  
 页眉和页脚显示在每个呈现的页面的顶部和底部。 您可以设置页眉和页脚的格式，使其具有边框颜色、边框样式和边框宽度。 此外，还可以添加背景色或背景图像。 根据所选格式，这些格式选项都会呈现出来。  
  
 以 HTML 或 MHTML 呈现格式呈现时，以下规则适用于页眉和页脚：  
  
> [!NOTE]  
>  有关 Excel 如何呈现页眉和页脚的信息，请参阅[导出到 Microsoft Excel（报表生成器和 SSRS）](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)。 有关 Word 如何呈现页眉和页脚的信息，请参阅[导出到 Microsoft Word（报表生成器和 SSRS）](../../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)。  
  
-   显示时，页眉和页脚分别呈现在可用页面区域内每一页的顶部和底部。  
  
-   在页眉或页脚隐藏的页面上，即使不呈现页眉或页脚，可用页面区域内仍然保留页眉或页脚的高度。  
  
-   如果页眉或页脚的内容增长到页眉或页脚的边界之外，则页眉或页脚的大小会增大以容纳这些内容。  
  
 以 PDF 或图像呈现格式呈现时，以下规则适用于页眉和页脚：  
  
-   页眉或页脚分别呈现在可用页面区域内每一页的顶部和底部。  
  
-   在页眉或页脚隐藏的页面上，即使不呈现页眉或页脚，可用页面区域内仍然保留页眉或页脚的高度。  
  
-   页眉和页脚不会增长，也不会缩减。 它们呈现在每一页上创建页眉或页脚时指定的高度处。  
  
-   不论报表内的列数如何，每一页只有一个页眉和页脚。  
  
-   如果页眉或页脚的内容增长到页眉或页脚的边界之外，将截断其内容。  
  
-   当报表呈现为子报表时，在原始 RDL 文件中定义的表头和表尾不会呈现出来。  
  
## <a name="logical-page-breaks"></a>逻辑分页符  
 逻辑分页符是在报表项或组之前或之后插入的分页符。 分页符有助于确定报表内容适合报表页的方式，以便在呈现或导出报表时获得最佳查看效果。  
  
 呈现逻辑分页符时应用以下规则：  
  
-   对于持续隐藏的报表项以及通过单击其他报表项来控制可见性的报表项，将忽略逻辑分页符。  
  
-   如果按条件可见的项在报表呈现时可见，则逻辑分页符应用于这些项。  
  
-   在具有逻辑分页符的报表项与对等报表项之间保留有间距。  
  
-   在报表项之前插入的逻辑分页符将报表项向下推至下一页。 该报表项将呈现在下一页的顶部。  
  
-   对表或矩阵单元中的项定义的逻辑分页符将不保留。 此逻辑分页符将不应用于列表中的项。  
  
## <a name="see-also"></a>另请参阅  
 [不同报表呈现扩展插件的交互功能（报表生成器和 SSRS）](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [以 HTML 格式呈现（报表生成器和 SSRS）](../../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md)   
 [页面布局和呈现方式（报表生成器和 SSRS）](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)  
  
  
