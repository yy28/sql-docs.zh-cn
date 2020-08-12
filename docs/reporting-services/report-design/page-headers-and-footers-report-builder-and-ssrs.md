---
title: 页眉和页脚（报表生成器）| Microsoft Docs
description: 发现可添加到页眉和页脚的多个项，包括文本、图像、矩形、边框、背景色和报表生成器中的表达式。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10125"
- sql13.rtp.rptdesigner.pagefooter.border.f1
- "10121"
- "10120"
- "10122"
- sql13.rtp.rptdesigner.pageheader.general.f1
- "10123"
- sql13.rtp.rptdesigner.pageheader.fill.f1
- sql13.rtp.rptdesigner.pageheader.border.f1
- sql13.rtp.rptdesigner.pagefooter.fill.f1
- sql13.rtp.rptdesigner.pagefooter.general.f1
- "10124"
ms.assetid: 4fb9faac-511e-404a-b8d7-1f2e3cb47b11
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ca788f2b86e2e71465228a7e00cf55efb86c8914
ms.sourcegitcommit: e572f1642f588b8c4c75bc9ea6adf4ccd48a353b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2020
ms.locfileid: "84778359"
---
# <a name="page-headers-and-footers-report-builder-and-ssrs"></a>页眉和页脚（报表生成器和 SSRS）
  报表可以包含页眉和页脚，它们分别位于每一页的顶部和底部。 页眉和页脚可以包含静态文本、图像、线条、矩形、边框、背景色、背景图像和表达式。 表达式包含只具有一个数据集的报表的数据集字段引用，以及作为作用域包括的数据集的聚合函数调用。  
  
> [!NOTE]  
>  各个呈现扩展插件对页的处理方式各不相同。 有关报表分页和呈现扩展插件的详细信息，请参阅[Reporting Services 中的分页（报表生成器和 SSRS）](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)。  
  
 默认情况下，报表有页脚，但没有页眉。 有关如何添加或删除它们的详细信息，请参阅[添加或删除页眉和页脚（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)。  
  
 页眉和页脚通常包含页码、报表标题和其他报表属性。 有关如何将这些项添加到报表报表头或报表尾的详细信息，请参阅[显示页码或其他报表属性（报表生成器和 SSRS）](../../reporting-services/report-design/display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md)。  
  
 创建页眉或页脚之后，即在每个报表页面上显示它们。 有关如何在第一页和最后一页上隐藏页眉和页脚的详细信息，请参阅[隐藏第一页或最后一页的页眉和页脚（报表生成器和 SSRS）](../../reporting-services/report-design/hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-headers-and-footers"></a>报表表头和表尾  
 页眉和页脚与报表表头和表尾有所不同。 报表没有特殊的报表表头或报表表尾区域。 报表表头由放置在报表设计图面上的表体顶部的报表项组成。 它们在报表中作为第一项内容仅出现一次。 报表表尾由放置在表体底部的报表项组成。 它们在报表中作为最后一项内容仅出现一次。  
  
## <a name="displaying-variable-data-in-a-page-header-or-footer"></a>在页眉或页脚中显示变量数据  
 页眉和页脚可以包含静态内容，不过它们更常用于显示变化的内容，例如页码或有关页面内容的信息。 若要在每个页上显示不同的变量数据，您必须使用表达式。  
  
 如果报表中仅定义了一个数据集，则可以向页眉或页脚添加简单表达式，例如 `[FieldName]` 。 将字段从“报表数据”窗格数据集字段集合或内置字段集合拖到页眉或页脚中。 系统会自动为您添加具有相应表达式的文本框。  
  
 若要计算页面上各个值的总和或其他聚合，可以使用指定 ReportItems 或数据集名称的表达式。 ReportItems 集合是显示报表呈现之后每页上的文本框集合。 报表定义中必须包含数据集名称。 下表显示了每种聚合表达式中所支持的项：  
  
|提供支持的表达式|ReportItems 聚合|数据集聚合（作用域必须是数据集名称）|  
|-----------------------------|----------------------------|----------------------------------------------------------|  
|表体中的文本框|是|否|  
|&PageNumber|是|否|  
|&TotalPages|是|否|  
|聚合函数|是的。 例如，<br /><br /> `=First(ReportItems!TXT_LastName.Value)`|是的。 例如，<br /><br /> `=Max(Quantity.Value,"DataSet1")`|  
|页面上各个项的字段集合|间接支持。 例如，<br /><br /> `=Sum(ReportItems!Textbox1.Value)`|是的。 例如，<br /><br /> `=Sum(Fields!Quantity.Value,"DataSet1")`|  
|数据绑定图像|间接支持。 例如： `=ReportItems!TXT_Photo.Value`|是的。 例如，<br /><br /> `=First(Fields!Photo.Value,"DataSet1")`|  
  
 本主题的以下部分介绍了在页眉和页脚中常用来获取变量数据的现成表达式。 还有一部分介绍 Excel 呈现扩展插件如何处理页眉和页脚。 有关表达式的详细信息，请参阅[表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)。  
  
### <a name="adding-calculated-page-totals-to-a-header-or-footer"></a>向页眉或页脚中添加计算出的页总计  
 对于某些报表，在每个报表的页眉或页脚中包括计算出的值非常有用；例如，如果页包括数值，则在每页上显示总计和。 由于无法直接引用字段，因此，放置到页眉或页脚中的表达式必须引用报表项（例如文本框）的名称，而不是引用数据字段：  
  
 `=Sum(ReportItems!Textbox1.Value)`  
  
 如果文本框位于包含重复数据行的表或列表中，则在运行时出现在页眉或页脚中的值将是当前页的表或列表中所有 `TextBox1` 实例数据的所有值之和。  
  
 在计算页总计时，使用不同的呈现扩展插件查看报表可能会显示不同的总计结果。 不同的呈现扩展插件会以不同的方式计算分页输出。 同一页在 HTML 中查看时可能会与在 PDF 中查看时显示不同的总计结果（如果 PDF 页上的数据量不同）。 有关详细信息，请参阅[呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
### <a name="for-reports-with-multiple-datasets"></a>对于具有多个数据集的报表  
 对于具有多个数据集的报表，无法直接向页眉或页脚中添加字段或数据绑定图像。 但是，可以编写表达式来间接引用要在页眉或页脚中使用的字段或数据绑定图像。  
  
 若要在页眉或页脚中放入变量数据，请执行以下操作：  
  
-   向页眉或页脚中添加文本框。  
  
-   在文本框中，编写生成要显示的变量数据的表达式。  
  
-   在表达式中，包括对页上报表项的引用；例如，可以引用包含特定字段的数据的文本框。 不要包括对数据集中的字段的直接引用。 例如，不能使用表达式 `[LastName]`。 可以使用以下表达式显示名为 `TXT_LastName`的文本框的第一个实例的内容：  
  
     `=First(ReportItems!TXT_LastName.Value)`  
  
 不能在页眉或页脚中对字段使用聚合函数。 只能对表体中的报表项使用聚合函数。 有关页眉和页脚中常用的表达式，请参阅[表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)。  
  
#### <a name="adding-a-data-bound-image-to-a-header-or-footer"></a>向页眉或页脚中添加数据绑定图像  
 可以在页眉或页脚中使用存储在数据库中的图像数据。 但是，不能直接从图像报表项引用数据库字段。 而是必须在表体中添加文本框，然后将文本框设置为包含图像的数据字段（注意，该值必须采用 base64 编码）。 可以在表体中隐藏该文本框以避免显示 base64 编码的图像。 然后，可以从页眉或页脚中的图像报表项引用隐藏文本框的值。  
  
 例如，假设有一个由产品信息页组成的报表。 您希望在每个页的页眉中显示产品的照片。 若要在报表表头中输出存储的图像，请在表体中定义一个名为 `TXT_Photo` 的隐藏文本框，用于从数据库检索图像，并使用表达式为该文本框赋值：  
  
 `=Convert.ToBase64String(Fields!Photo.Value)`  
  
 在页眉中，添加一个使用 `TXT_Photo` 文本框的图像报表项，解码后用于显示图像：  
  
 `=Convert.FromBase64String(ReportItems!TXT_Photo.Value)`  
  
## <a name="using-headers-and-footers-to-position-text"></a>使用页眉和页脚放置文本  
 可以使用页眉和页脚在页上放置文本。 例如，假设正在创建要通过邮件发送给客户的报表。 可以使用页眉或页脚来放置客户地址，以便在折叠时该地址会出现在信封窗口中。  
  
 如果文本框只用来填充页眉或页脚，则可以在表体中隐藏该文本框。 文本框在表体中的位置会影响该值是出现在报表的第一页的页眉或页脚中还是出现在最后一页的页眉或页脚中。 例如，如果有会导致报表跨越多页的表、矩阵或列表，则隐藏文本框的值将出现在最后一页上。 若要使其出现在第一页上，请将隐藏文本框放在表体的顶部。  
  
## <a name="designing-reports-with-page-headers-and-footers-for-specific-renderers"></a>设计带有特定呈现器的页眉和页脚的报表  
 处理报表时，数据和布局信息将组合在一起。 查看报表时，组合信息被传递到呈现器，确定每个报表页面上能够容纳的报表数据量。  
  
 如果使用浏览器查看报表服务器上的报表，HTML 呈现器控制在每个报表页面上显示的内容。 如果打算以不同于查看的格式来传递报表，或者如果打算以特定格式打印报表，可能需要优化用于最终报表格式的呈现器的报表布局。 有关报表分页的详细信息，请参阅[Reporting Services 中的分页（报表生成器和 SSRS）](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)。  
  
### <a name="working-with-page-headers-and-footers-in-excel"></a>在 Excel 中使用页眉和页脚  
 在为面向 Excel 呈现扩展插件的报表定义页眉和页脚时，请遵循以下原则以获得最佳的结果：  
  
-   使用页脚显示页码。  
  
-   使用页眉显示图像、标题或其他文本。 不要将页码放在页眉中。  
  
 在 Excel 中，页脚的布局受到限制。 如果所定义的报表在页脚中包括复杂的报表项，则在 Excel 中查看报表时，页脚不会按您所期望的方式进行处理。  
  
 Excel 呈现扩展插件可以在页眉中容纳图像并允许在页眉中对简单或复杂的报表项进行绝对定位。 支持更丰富的页眉布局的副作用是在页眉中不再支持计算页码。 在 Excel 呈现扩展插件中，默认设置是根据工作表的数量来计算页码。 根据定义报表的方式，这可能产生错误的页码。 例如，假设一个报表呈现为可分四页打印的单个大型工作表。 如果在页眉中包括页码信息，则在打印的每个页的页眉中将显示“第 1 页，共 1 页”。  
  
 根据与打印页的尺寸相关的逻辑页数，可以生成更准确的页计数。 在 Excel 中，页脚会自动使用逻辑页码。 若要将逻辑页计数放在页眉中，必须将设备信息设置配置为使用简单页眉。 注意，使用简单页眉时，将删除在页眉区域中处理复杂报表布局的功能。  
  
 有关详细信息，请参阅 [导出到 Microsoft Excel（报表生成器和 SSRS）](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)中处理数据。  
  
## <a name="see-also"></a>另请参阅  
 [在报表中嵌入图像（报表生成器和 SSRS）](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [矩形和线条（报表生成器和 SSRS）](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)  
  
  
