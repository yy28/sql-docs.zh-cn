---
title: "\"处理\" 对话框（Analysis Services 多维数据） |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.processdialog.f1
ms.assetid: c065248c-9001-4f0c-928f-9c59eccb618b
author: minewiskan
ms.author: owend
ms.openlocfilehash: f6b9ab6db9fc50b09b752b5deaa59d42c4664bd5
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539987"
---
# <a name="process-dialog-box-analysis-services---multidimensional-data"></a>“处理”对话框（Analysis Services - 多维数据）
  可以使用 **和** 中的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] “处理” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 对话框处理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象。 在 **中，可以执行以下操作以显示** “处理” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 对话框：  
  
-   在“解决方案资源管理器”中右键单击某个 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目、多维数据集、维度或挖掘结构，然后选择“处理”********。  
  
-   在 **多维数据集设计器** 的所有页、 **维度设计器**的所有页或 **数据挖掘模型设计器**的 **“挖掘结构”** 和 **“挖掘模型”** 页上，从工具栏中选择 **“处理”**。  
  
-   在“数据挖掘模型设计器”的“挖掘模型”页中，右键单击某个挖掘模型，然后选择“处理挖掘结构和所有模型”或“处理模型”****************。  
  
 在 **SQL Server Management Studio** 中，可以通过执行以下操作显示 **“处理”** 对话框：  
  
-   在“对象资源管理器”中右键单击某个 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库、多维数据集、度量值组、分区、维度、挖掘结构或挖掘模型，然后选择“处理”********。  
  
## <a name="options"></a>选项  
 **对象列表**  
 选择要处理的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象和要应用的处理选项及设置。 该网格包含以下列：  
  
 **Object Name**  
 显示要处理的对象的名称。 名称左侧的图标指示对象类型。  
  
 类型  
 显示要处理的对象的类型。  
  
 **处理选项**  
 选择要对所选对象执行的处理类型。 有关可用的处理选项的详细信息，请参阅[多维模型对象处理](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 **设置**  
 对于多维数据集、度量值组或分区，在“处理选项”中选择“处理增量”时，会显示“配置”超链接************。 单击 **“配置”** 可启动 **“增量更新”** 对话框。 有关“增量更新”**** 对话框的详细信息，请参阅[“增量更新”对话框（Analysis Services - 多维数据）](incremental-update-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **移除**  
 单击此项可从****“对象列表”中删除所选项。  
  
 **影响分析**  
 单击此项可打开“影响分析”**** 对话框，并显示将被处理任务影响的对象。 有关****“影响分析”对话框的详细信息，请参阅[“影响分析”对话框（Analysis Services - 多维数据）](impact-analysis-dialog-box-analysis-services-multidimensional-data.md)。  
  
> [!NOTE]  
>  当在“更改设置”对话框中选中“处理影响的对象”选项时，将禁用此选项********。  
  
 **更改设置**  
 单击此项可打开****“更改设置”对话框，并更改用于控制所选对象的处理方式的设置，包括批处理设置、写回设置、维度键错误设置。 有关“更改设置”**** 对话框的详细信息，请参阅[“更改设置”对话框（Analysis Services - 多维数据）](change-settings-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **运行**  
 单击此项可处理对象。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;多维数据的 Analysis Services 设计器和对话框&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 ["处理进度" 对话框 &#40;Analysis Services 多维数据&#41;](process-progress-dialog-box-analysis-services-multidimensional-data.md)  
  
  
