---
title: 针对 DMX 的 Analysis Services 连接类型 (SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- parameters [Reporting Services], DMX
- Data Mining Prediction [Reporting Services]
- query view [Reporting Services]
- DMX [Reporting Services]
- design view [Reporting Services]
- data mining [Reporting Services]
- passing parameters [Reporting Services]
ms.assetid: 2de825e9-6d8a-4128-add0-da15dc6cea3e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cde09f46f702a6d1df6fba57feb52fb7f9e25928
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43265155"
---
# <a name="analysis-services-connection-type-for-dmx-ssrs"></a>针对 DMX 的 Analysis Services 连接类型 (SSRS)
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源创建数据集时，如果检测到有效多维数据集，则报表设计器将显示多维表达式 (MDX) 查询设计器。 如果未检测到多维数据集，但有数据挖掘模型可用，则报表设计器将会显示数据挖掘扩展插件 (DMX) 查询设计器。 要在 MDX 和 DMX 设计器之间切换，请单击工具栏上的“命令类型 DMX”（![更改为 DMX 查询语言视图](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "Change to DMX query language view")）按钮。 使用 DMX 查询设计器以交互方式生成使用图形元素的 DMX 查询。 若要使用 DMX 查询设计器，指定的数据源必须已具有可提供数据的数据挖掘模型。 查询结果被转换为要在报表中使用的平展行集。  
  
> [!NOTE]  
>  在设计报表前必须为模型定型。 有关详细信息，请参阅 [数据挖掘解决方案](../../analysis-services/data-mining/data-mining-solutions.md)。  
  
## <a name="design-mode"></a>设计模式  
 DMX 查询设计器将在设计模式下打开。 设计模式包含用于选择单个数据挖掘模型和输入表的图形设计图面，同时还包含用于指定预测查询的网格。 DMX 查询设计器还有其他两种模式：查询模式和结果模式。 在查询模式中，查询窗格取代了设计模式中的网格，您可以在查询窗格中键入 DMX 查询。 在结果模式中，由查询返回的结果集显示在数据网格中。  
  
 要更改 DMX 查询设计器的模式，请右键单击查询设计图面，并选择“设计”、“查询”或“结果”。 有关详细信息，请参阅 [Analysis Services DMX 查询设计器用户界面](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)和[从数据挖掘模型 (DMX) 检索数据 (SSRS)](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md)。  
  
## <a name="designing-a-prediction-query"></a>设计预测查询  
 设计模式的“查询设计”窗格中包含两个窗口： **“挖掘模型”** 和 **“选择输入表”**。 使用 **“挖掘模型”** 窗口可选择要在查询中使用的挖掘模型。 使用 **“选择输入表”** 窗口可选择预测所基于的表。 如果希望使用单独查询而不是输入表，请在“查询设计”窗格中右键单击，并选择“单独查询”。 **“单独查询输入”** 窗口将取代 **“选择输入表”** 窗口。  
  
 在设计模式中，可以将 **“挖掘模型”** 窗口和 **“选择输入表”** 窗口中的字段拖至“网格”窗格中的 **“字段”** 列。 您还可以填充其余列来指定别名、在结果中显示字段、将字段组合在一起以及指定运算符根据给定条件或参数限制字段值。 如果使用的是查询模式，请通过将字段拖至“查询”窗格来生成 DMX 查询。  
  
## <a name="using-parameters"></a>使用参数  
 您可以将报表参数传递到 DMX 查询参数。 若要如此操作，必须向 DMX 查询添加一个参数，在 **“查询参数”** 对话框中定义相应的查询参数，再修改相关联的报表参数。 要定义查询参数，请单击工具栏上的“查询参数”（![“查询参数”对话框图标](../../reporting-services/report-data/media/iconqueryparameter.gif "“查询参数”对话框图标")）按钮。 若要查看有关在 DMX 查询中定义参数的说明，请参阅[在 Analysis Services 的 MDX 查询设计器中定义参数（报表生成器和 SSRS）](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md)  
  
 有关如何管理报表参数与查询参数之间关系的详细信息，请参阅[将查询参数与报表参数关联（报表生成器和 SSRS）](../../reporting-services/report-data/associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md)。 有关参数的详细信息，请参阅[报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘解决方案](../../analysis-services/data-mining/data-mining-solutions.md)   
 [查询设计工具 (SSRS)](../../reporting-services/report-data/query-design-tools-ssrs.md)   
 [数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
