---
title: 导出到 CSV 文件（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 68ec746e-8c82-47f5-8c3d-dbe403a441e5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: eece2e47cee99c1c3716aadc597e8b6e6dd48d79
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65581210"
---
# <a name="exporting-to-a-csv-file-report-builder-and-ssrs"></a>导出到 CSV 文件（报表生成器和 SSRS）
  逗号分隔值 (CSV) 呈现扩展插件以平展的表示形式呈现分页报表中的数据，格式为标准化的纯文本，这种数据表示形式容易读取且可与多个应用程序交换。  
  
 CSV 呈现扩展插件使用字符串分隔符来分隔字段和行，字符串分隔符可以配置为逗号之外的其他字符。 生成的文件可以用电子表格程序（如 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] ）打开，也可以用作其他程序的导入格式。 所导出的报表会变为 .csv 文件，并返回 MIME 类型的 **text/csv**。  
  
 如果您想要在 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)]中处理与图表、数据条、迷你图、仪表和指示器相关的数据，请将报表导出为 CSV 文件，然后在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 中打开该文件。  
  
 有关如何导出为 CSV 格式的详细信息，请参阅[导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="CSVRendering"></a> CSV 呈现  
 当使用默认设置进行呈现时，CSV 报表具有以下特征：  
  
-   默认字段分隔符字符串是逗号 (,)。  
  
    > [!NOTE]  
    >  可通过更改设备信息设置将字段分隔符更改为任何所需的字符，包括 TAB。 有关详细信息，请参阅 [CSV Device Information Settings](../../reporting-services/csv-device-information-settings.md)。  
  
-   记录分隔符字符串是回车符和换行符 (\<cr>\<lf>)。  
  
-   文本限定符字符串是引号 (")。  
  
     CSV 呈现器不在所有文本字符串周围添加限定符。 只有在值包含分隔符或值具有换行符时才会添加文本限定符。  
  
-   如果文本包含嵌入的分隔符字符串或限定符字符串，则会用文本限定符（引号）将该文本括起来，还将嵌入的限定符字符串（引号）用引号引起来。  
  
-   忽略格式设置和布局。  
  
 在呈现期间会忽略以下项：  
  
-   页眉  
  
-   页脚  
  
-   自定义报表项  
  
-   行  
  
-   映像  
  
-   Rectangle  
  
-   自动小计  
  
 对其余的报表项进行排序，先从上到下排，再从左到右排。 之后，每一项将呈现到一列中。 如果报表有嵌套数据项（如列表或表），则会在每条记录中重复它的父项。  
  
 下表说明了呈现报表项时这些报表项的外观：  
  
|Item|呈现行为|  
|----------|------------------------|  
|文本框|呈现文本框的内容。 在默认模式下，会根据项的格式设置属性对其进行格式化。 在兼容模式下，可以根据设备信息设置对格式进行更改。 有关 CSV 呈现模式的详细信息，请参阅下文。|  
|表|呈现方式为扩展该表，在只保留最起码的格式的情况下为每一行和每一列都分别创建行和列。 小计行和小计列没有列标题或行标题。 不支持钻取报表。|  
|矩阵|呈现方式为扩展该矩阵，在只保留最起码的格式的情况下为每一行和每一列都分别创建行和列。 小计行和小计列没有列标题或行标题。|  
|列出|为列表中每一明细行或实例呈现一个记录。|  
|子报表|对于内容的每个实例，都会重复它的父项。|  
|图表|通过创建每个图表值的行和成员标签来呈现。 来自系列和类别的标签采用平展的层次结构，并包含在图表值的行中。|  
|数据条|像图表一样呈现。 通常，数据条并不包括层次结构或标签。|  
|迷你图|像图表一样呈现。 通常，迷你图并不包括层次结构或标签。|  
|仪表|作为单个记录呈现，具有线性刻度的最小值和最大值、范围的起始和终止值，以及指针的值。|  
|指示器|作为单个记录呈现，具有活动状态名称、可用状态以及数据值。|  
|映射|对于地图层的每个地图成员，呈现包含标签和值的行。<br /><br /> 如果地图具有多个层，则行中的值将会变化，具体取决于地图层是使用相同还是不同的地图数据区域。 如果多个地图层使用相同数据区域，该行将包含所有层的数据。|  
  
### <a name="hierarchical-and-grouped-data"></a>分层数据和分组数据  
 分层数据和分组数据必须进行平展才能以 CSV 格式表示。  
  
 呈现扩展插件可将报表平展为用于表示数据区域中嵌套组的树结构。 要平展报表：  
  
-   行层次结构在列层次结构之前进行平展。  
  
-   列按照以下顺序排序：表体中的文本框的顺序为从左到右，从上到下，后面紧跟数据区域，后者顺序为从左到右，从上到下。  
  
-   在数据区域中，列按照以下顺序排序：角成员、行层次结构成员、列层次结构成员，然后是单元。  
  
-   对等数据区域是一些共享一个公共数据区域或动态祖先的数据区域或动态组。 对等数据通过平展后的树的分支进行标识。  
  
 有关详细信息，请参阅 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)。  
  
  
##  <a name="RenderingModes"></a> 呈现器模式  
 CSV 呈现扩展插件可在两种模式下运行：一种模式针对 Excel 进行了优化，另一种模式针对要求严格遵守 RFC 4180 中的 CSV 规范的第三方应用程序进行了优化。 根据所用模式的不同，对等数据区域的处理方式也有所不同。  
  
### <a name="default-mode"></a>默认模式  
 默认模式针对 Excel 进行了优化。 使用默认模式呈现时，报表将呈现为带多个以 CSV 格式呈现的数据部分的 CSV 文件。 每个对等数据区域均由一个空行分隔。 表体中的各对等数据区域呈现为 CSV 文件中的独立数据块。 呈现结果为 CSV 文件，在该 CSV 文件中：  
  
-   表体中的各个文本框均作为 CSV 文件中的第一个数据块呈现，只呈现一次。  
  
-   表体中的每个顶级对等数据区域在其各自的数据块中呈现。  
  
-   嵌套数据区域会沿对角线呈现到同一数据块中。  
  
#### <a name="formatting"></a>格式设置  
 数值按照其格式化后的状态呈现。 Excel 可识别经过格式化的数值（例如货币、百分比和日期），并可在导入 CSV 文件时对单元进行合适的格式化。  
  
### <a name="compliant-mode"></a>兼容模式  
 兼容模式针对第三方应用程序进行了优化。  
  
#### <a name="data-regions"></a>数据区域  
 只有文件的第一行包含列标题，并且每一行均具有数目相同的列。  
  
#### <a name="formatting"></a>格式设置  
 值未经过格式化。  
  
##  <a name="Interactivity"></a> 交互  
 此呈现器生成的两种 CSV 格式都不支持交互。 不会呈现以下交互元素：  
  
-   超链接  
  
-   显示或隐藏  
  
-   文档结构图  
  
-   钻取链接或点击链接  
  
-   最终用户排序  
  
-   修复标题  
  
-   书签  
  
  
##  <a name="DeviceInfo"></a> 设备信息设置  
 您可以通过更改设备信息设置来更改相应呈现器的某些默认设置，包括呈现使用的模式、用作分隔符的字符以及用作文本限定符默认字符串的字符。 有关详细信息，请参阅 [CSV Device Information Settings](../../reporting-services/csv-device-information-settings.md)。  
  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 中的分页（报表生成器和 SSRS）](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同报表呈现扩展插件的交互功能（报表生成器和 SSRS）](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [呈现报表项（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
