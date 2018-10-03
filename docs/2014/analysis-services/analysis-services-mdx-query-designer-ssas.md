---
title: Analysis Services MDX 查询设计器 (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.asmdxquerydes.f1
ms.assetid: a2fb0b79-802a-4dac-bd9a-32dfe2e8c4d4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 89818073559b3a6b6faab919691a62899b442e3e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113417"
---
# <a name="analysis-services-mdx-query-designer-ssas"></a>Analysis Services MDX 查询设计器 (SSAS)
  Analysis Services 多维表达式 (MDX) 查询设计器提供了图形用户界面，可帮助你为 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据源创建 MDX 查询。 MDX 图形查询设计器有两种模式：设计模式和查询模式。 每种模式都提供一个“元数据”窗格，从该窗格中可以拖动所选多维数据集的成员，以生成可检索要使用的数据的 MDX 查询。  
  
> [!IMPORTANT]  
>  用户创建和运行查询时访问数据源。 您应授予对数据源的最小权限（如只读权限）。  
>   
>  在执行查询时，当前用户的凭据（而非在“模拟信息”页中指定的凭据）用于连接到数据源并提取数据。  
  
 以下几节介绍每种模式的图形查询设计器中的工具栏按钮和查询设计器窗格。  
  
## <a name="graphical-mdx-query-designer-in-design-mode"></a>设计模式下的图形 MDX 查询设计器  
 编辑 MDX 查询时，图形 MDX 查询设计器将以设计模式打开。  
  
 下图列出了设计模式的窗格。  
  
 ![Analysis Services MDX 查询设计器，设计视图](media/rsqd-dsawas-mdx-designmode.gif "Analysis Services MDX query designer, design view")  
  
 下表列出了查询模式下的窗格：  
  
|Pane|函数|  
|----------|--------------|  
|选择“多维数据集”按钮 (**...**)|显示当前选定的多维数据集。|  
|“元数据”窗格|显示在选定多维数据集中定义的度量值、关键绩效指标 (KPI) 和维度的层次列表。|  
|“计算成员”窗格|显示当前定义的可在查询中使用的计算成员。|  
|“筛选器”窗格|用于选择维度和相关的层次结构，以筛选源中的数据并限制返回的数据。|  
|“数据”窗格|在从“元数据”窗格向“计算成员”窗格拖动项目时，显示结果集的列标题。 如果选中 **“自动执行”** 按钮，则可自动更新结果集。|  
  
 可以将“元数据”窗格中的维度、度量值和 KPI 以及“计算成员”窗格中的计算成员拖至“数据”窗格。 在“筛选器”窗格中，您可以选择维度和相关的层次结构，并设置筛选器表达式以限制可用于查询的数据。 如果选中工具栏上的“自动执行”（![自动执行查询](media/rsqdicon-autoexecute.gif "AutoExecute the query")）切换按钮，则每次将元数据对象拖到“数据”窗格时，查询设计器都将运行查询。 可以使用工具栏上的“运行”（![运行查询](media/rsqdicon-run.gif "Run the query")）按钮手动运行查询。  
  
 在此模式下创建 MDX 查询时，下面的附加属性将会自动包含到查询中：  
  
 **成员属性** MEMBER_CAPTION, MEMBER_UNIQUE_NAME  
  
 **单元属性** VALUE、BACK_COLOR、FORE_COLOR、FORMATTED_VALUE、FORMAT_STRING、FONT_NAME、FONT_SIZE、FONT_FLAGS  
  
 若要指定您自己的附加属性，则必须在查询模式下，手动编辑 MDX 查询。  
  
 不支持从文件导入 .mdx 查询。  
  
> [!NOTE]  
>  有关 MDX 的详细信息以及有关 MDX 查询设计器的常规信息，请参阅 [SQL Server 联机丛书](http://go.microsoft.com/fwlink/?linkid=98335)中的“MDX 查询编辑器（Analysis Services - 多维数据）”。  
  
### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>设计模式下的图形 MDX 查询设计器工具栏  
 查询设计器工具栏提供了可以帮助您使用图形界面来设计 MDX 查询的按钮。 下表列出了这些按钮及其功能。  
  
|按钮|Description|  
|------------|-----------------|  
|**编辑为文本**|不可用于此数据源类型。|  
|**导入**|从文件系统中的报表定义 (.rdl) 文件导入现有查询。|  
|![更改为 MDX 查询视图](media/rsqdicon-commandtypemdx.gif "Change to MDX query view")|切换到命令类型 MDX。|  
|![刷新结果数据](media/rsqdicon-refresh.gif "Refresh result data")|刷新数据源的元数据。|  
|![添加计算的成员](media/rsqdicon-addcalculatedmember.gif "添加计算的成员")|显示 **“计算成员生成器”** 对话框。|  
|![切换显示空单元格](media/rsqdicon-showemptycells.gif "Toggle for show empty cells")|在“数据”窗格中的显示或不显示空单元格之间切换。 （这等同于在 MDX 中使用 NON EMPTY 子句）。|  
|![自动执行查询](media/rsqdicon-autoexecute.gif "AutoExecute the query")|在每次进行更改时自动运行查询并显示结果。 结果将显示在“数据”窗格中。|  
|![“显示聚合”按钮](media/rsqdicon-showaggregations.gif "Show Aggregations button")|在“数据”窗格中显示聚合。|  
|![删除](media/rsqdicon-delete.gif "删除")|通过查询在“数据”窗格中删除选定列。|  
|![“查询参数”对话框图标](media/iconqueryparameter.gif "Icon for the Query Parameters dialog box")|显示 **“查询参数”** 对话框。 指定查询参数的值时，会自动创建一个同名参数。|  
|![“准备查询”按钮](media/rsqdicon-preparequery.gif "“准备查询”按钮")|准备查询。|  
|![运行查询](media/rsqdicon-run.gif "运行查询")|运行查询并在“数据”窗格中显示结果。|  
|![取消查询](media/rsqdicon-cancel.gif "Cancel the query")|取消查询。|  
|![切换到设计模式](media/rsqdicon-designmode.gif "Switch to Design mode")|在设计模式和查询模式之间切换。|  
  
## <a name="graphical-mdx-query-designer-in-query-mode"></a>查询模式下的图形 MDX 查询设计器  
 若要将图形查询设计器更改为 **“查询”** 模式，请单击工具栏上的 **“设计模式”** 按钮。  
  
 下图列出了查询模式的窗格。  
  
 ![Analysis Services MDX 查询设计器，查询视图](media/rsqd-dsawas-mdx-querymode.gif "Analysis Services MDX query designer, query view")  
  
 下表列出了查询模式下的窗格：  
  
|Pane|函数|  
|----------|--------------|  
|选择“多维数据集”按钮 (**...**)|显示当前选定的多维数据集。|  
|元数据/函数/模板窗格|显示在选定多维数据集中定义的度量值、KPI 和维度的层次列表。|  
|“查询”窗格|显示查询文本。|  
|“结果”窗格|显示运行查询的结果。|  
  
 “元数据”窗格会显示 **“元数据”** 选项卡、 **“函数”** 选项卡和 **“模板”** 选项卡。 通过 **“元数据”** 选项卡，可将维度、层次结构、KPI 和度量值拖到“MDX 查询”窗格中。 通过 **“函数”** 选项卡，可将函数拖到“MDX 查询”窗格中。 通过 **“模板”** 选项卡，可将 MDX 模板添加到“MDX 查询”窗格中。 执行查询时，“结果”窗格将显示 MDX 查询的结果。  
  
 您可以扩展设计模式下生成的默认 MDX 查询，以包含附加成员属性和单元属性。 运行查询时，这些值不会显示在结果集中。 不过，这些值会随同数据集字段集合传递回来，并且您可以使用这些值。  
  
### <a name="graphical-query-designer-toolbar-in-query-mode"></a>查询模式下的图形查询设计器工具栏  
 查询设计器工具栏提供了可以帮助您使用图形界面来设计 MDX 查询的按钮。  
  
 工具栏按钮在设计模式和查询模式下是相同的，但是下列按钮在查询模式下不可用：  
  
-   **编辑为文本**  
  
-   **添加计算成员**(![添加计算的成员](media/rsqdicon-addcalculatedmember.gif "添加计算的成员"))  
  
-   **显示空单元格**（![切换显示空单元格](media/rsqdicon-showemptycells.gif "Toggle for show empty cells")）  
  
-   **自动执行**（![自动执行查询](media/rsqdicon-autoexecute.gif "AutoExecute the query")）  
  
-   **显示聚合**（![“显示聚合”按钮](media/rsqdicon-showaggregations.gif "Show Aggregations button")）  
  
  
