---
title: Analysis Services DMX 查询设计器用户界面 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10012"
- sql12.rtp.rptdesigner.dataview.asquerydesigner.f1
helpviewer_keywords:
- Analysis Services [DMX]
- DMX [Analysis Services], user interface
- query designers [DMX]
ms.assetid: 5fd726a4-aed7-4e6c-9404-ccb2db66cf26
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0d43ce55186f9545c1eb237620960fb678a4f402
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68891307"
---
# <a name="analysis-services-dmx-query-designer-user-interface"></a>Analysis Services DMX 查询设计器用户界面
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]提供图形查询设计器，用于为[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据源生成数据挖掘表达式（DMX）查询和多维表达式（MDX）查询。 该主题介绍了 DMX 查询设计器。 有关 MDX 查询设计器的详细信息，请参阅 [Analysis Services MDX Query Designer User Interface](analysis-services-mdx-query-designer-user-interface.md)。  
  
 DMX 图形查询设计器有三种模式：设计、查询和结果。 若要切换模式，用右键单击“查询设计”窗格，并选择模式。 每种模式都提供一个“元数据”窗格，从该窗格中可以拖动选定的多维数据集的成员，以创建可在处理报表时为数据集检索数据的 DMX 查询。  
  
## <a name="graphical-dmx-query-designer-toolbar"></a>图形 DMX 查询设计器工具栏  
 查询设计器工具栏提供了可以帮助您使用图形界面来设计 DMX 查询的按钮。 下表介绍了这些按钮及其功能。  
  
|按钮|说明|  
|------------|-----------------|  
|**编辑为文本**|对此数据源类型禁用。|  
|**Import**|从文件系统中的报表定义 (.rdl) 文件导入现有查询。 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。|  
|![更改为 MDX 查询视图](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-commandtypemdx.gif "更改为 MDX 查询视图")|切换到 MDX 查询设计器模式。|  
|![更改为 DMX 查询语言视图](../media/rsqdicon-commandtypedmx.gif "更改为 DMX 查询语言视图")|切换到 DMX 查询设计器模式。|  
|![刷新结果数据](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-refresh.gif "刷新结果数据")|刷新数据源的元数据。|  
|![删除](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-delete.gif "删除")|通过查询在“数据”窗格中删除选定列。|  
|![“查询参数”对话框图标](https://docs.microsoft.com/analysis-services/analysis-services/media/iconqueryparameter.gif "“查询参数”对话框图标")|显示 **“查询参数”** 对话框。 如果向变量分配了默认值，则当在报表设计器中切换到“布局”视图时，将创建相应的报表参数。|  
|![运行查询](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-run.gif "运行查询")|准备查询。|  
|![切换到设计模式](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-designmode.gif "切换到设计模式")|在设计模式和查询模式之间切换。 若要更改为结果视图，请右键单击“设计”窗格并选择“结果”****。|  
  
## <a name="graphical-dmx-query-designer-in-design-mode"></a>设计模式下的图形 DMX 查询设计器  
 编辑使用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据源的数据集（该数据集没有有效的多维数据集，但是具有有效的挖掘模型）时，将在设计模式下打开图形查询设计器。 下图列出了设计模式的窗格。  
  
 ![Analysis Services DMX 查询设计器，设计视图](../media/rsqd-dsawas-dmx-designmode.gif "Analysis Services DMX 查询设计器，设计视图")  
  
 下表介绍了每个窗格的功能。  
  
|窗格|函数|  
|----------|--------------|  
|“查询设计器”窗格|使用 **“挖掘模型”** 和 **“选择输入表”** 对话框创建 DMX 查询。|  
|网格窗格|使用“源”下拉列表为网格中的每行选择一个函数或表达式，并选择要用于 DMX 查询的字段、组以及条件或参数****。 若要查看根据您的选择生成的 DMX 查询文本，请单击工具栏中的 **“设计模式”** 按钮。|  
  
 若要运行 DMX 查询并在“结果”窗格中显示结果，请右键单击“查询设计”窗格并选择“结果”****。  
  
## <a name="graphical-dmx-query-designer-in-query-mode"></a>查询模式下的图形 DMX 查询设计器  
 若要将图形查询设计器更改为查询模式，请单击工具栏上的“设计模式”按钮，或右键单击查询设计界面，并从快捷菜单中选择“查询”********。 使用该模式直接在“查询”窗格中输入 DMX 文本。  
  
 下图列出了查询模式的窗格。  
  
 ![Analysis Services DMX 查询设计器，查询视图](../media/rsqd-dsawas-dmx-querymode.gif "Analysis Services DMX 查询设计器，查询视图")  
  
 下表介绍了每个窗格的功能。  
  
|窗格|函数|  
|----------|--------------|  
|“查询设计器”窗格|使用 **“挖掘模型”** 和 **“选择输入表”** 对话框创建 DMX 查询。|  
|“查询”窗格|直接在窗格中查看或编辑 DMX 查询文本。 如果重新回到 **“设计”** 模式，对 DMX 查询文本所做的更改将不再存在。|  
  
 若要运行 DMX 查询并在“结果”窗格中显示结果，请右键单击“查询设计”窗格并选择“结果”****。  
  
## <a name="graphical-dmx-query-designer-in-result-mode"></a>结果模式下的图形 DMX 查询设计器  
 若要显示结果模式，请右键单击查询设计图面并从快捷菜单中选择“结果”****。 切换到结果模式时，将自动运行 DMX 查询。  
  
 下图显示结果模式下的查询设计器。  
  
 ![Analysis Services DMX 查询设计器，结果视图](../media/rsqd-dsawas-dmx-resultmode.gif "Analysis Services DMX 查询设计器，结果视图")  
  
 若要切换回设计模式或查询模式，请右键单击“结果”窗格并选择“设计”或“查询”。********  
  
## <a name="see-also"></a>另请参阅  
 [在 MDX 查询设计器中为 Analysis Services &#40;报表生成器和 SSRS 定义参数&#41;](define-parameters-in-the-mdx-query-designer-for-analysis-services.md)   
 [创建共享数据集或嵌入数据集 &#40;报表生成器和 SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [DMX &#40;SSRS 的 Analysis Services 连接类型&#41;](analysis-services-connection-type-for-dmx-ssrs.md)   
 [从数据挖掘模型检索数据 &#40;DMX&#41; &#40;SSRS&#41;](retrieve-data-from-a-data-mining-model-dmx-ssrs.md)   
 [RSReportDesigner 配置文件](../report-server/rsreportdesigner-configuration-file.md)   
 [MDX &#40;Analysis Services 连接类型&#41;](analysis-services-connection-type-for-mdx-ssrs.md)   
 [DMX &#40;SSRS 的 Analysis Services 连接类型&#41;](analysis-services-connection-type-for-dmx-ssrs.md)  
  
  
