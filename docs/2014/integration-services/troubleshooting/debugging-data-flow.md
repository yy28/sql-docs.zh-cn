---
title: 调试数据流 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- progress reporting [Integration Services]
- data viewers [Integration Services]
- data flow [Integration Services], debugging
- debugging [Integration Services], data flow
- counting rows
ms.assetid: 1c574f1b-54f7-4c05-8e42-8620e2c1df0f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fdfaeeb9e8dafe82a1312593df2dd128635b8365
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391076"
---
# <a name="debugging-data-flow"></a>调试数据流
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器包含可用于解决 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包中数据流问题的功能和工具。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器提供数据查看器。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 转换提供行计数。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器在运行时提供进度报告。  
  
## <a name="data-viewers"></a>数据查看器  
 数据查看器显示数据流中两个组件间的数据。 当数据从数据源提取出来并首次进入数据流时、转换对数据进行更新前后以及数据加载到其目标之前，数据查看器均可显示数据。  
  
 若要查看数据，请将数据查看器附加到连接两个数据流组件的路径。 在数据流组件间查看数据的能力，使得确定异常数据值、查看转换更改列值的方式以及发现转换失败的原因变得更加简单。 例如，您可能发现引用表中的查找失败，而为更正此问题，可以添加一个为空列提供默认数据的转换。  
  
 数据查看器可以在网格中显示数据。 若使用网格方式，则选择要显示的列。 选定列的值以表格的格式显示。  
  
 您还可以在一个路径上包含多个数据查看器。 可以用不同的格式显示相同的数据（例如，为数据创建一个图表视图和一个网格视图），也可以为不同的数据列创建不同的数据查看器。  
  
 在将数据查看器添加到路径时， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器会将数据查看器图标添加到 **“数据流”** 选项卡的设计图面中，紧临该路径。 可具有多个输出的转换（如有条件拆分转换）可以在每个路径上包含一个数据查看器。  
  
 在运行时， **“数据查看器”** 窗口会打开，并显示由数据查看器格式所指定的信息。 例如，使用网格格式的数据查看器会显示选定列的数据、传递到数据流组件的输出行的行数以及所显示的行数。 信息按缓冲显示，根据数据流中的行的宽度，缓冲可以包含较多或较少的行。  
  
 在 **“数据查看器”** 对话框中，可以将数据复制到剪贴板、从表中清除所有数据、重新配置数据查看器、恢复数据流，以及分离或附加数据查看器。  
  
#### <a name="to-add-a-data-viewer"></a>添加数据查看器  
  
-   [将数据查看器添加到数据流](../add-a-data-viewer-to-a-data-flow.md)  
  
## <a name="row-counts"></a>行计数  
 通过路径已传递的行的数量在 **设计器中的** “数据流” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 选项卡的设计图面上紧临该路径显示。 随着数据在路径中的移动，该数量会定期更新。  
  
 您还可以将行计数转换添加到数据流中，以捕获变量中的最终行计数。 有关详细信息，请参阅 [Row Count Transformation](../data-flow/transformations/row-count-transformation.md)。  
  
## <a name="progress-reporting"></a>进度报告  
 在运行包时， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器用指示状态的颜色显示每个数据流组件，以此在 **“数据流”** 选项卡设计图面上描绘进度。 当每个组件开始执行其工作时，颜色由无色变为黄色，而在成功完成后，则变为绿色。 红色指示组件失败。  
  
 下表介绍颜色编码。  
  
|颜色|Description|  
|-----------|-----------------|  
|无色|等待被数据流引擎调用。|  
|Yellow|正在执行转换、提取数据或加载数据。|  
|绿色|成功运行。|  
|红色|运行中出现错误。|  
  
## <a name="see-also"></a>请参阅  
 [包开发的故障排除工具](troubleshooting-tools-for-package-development.md)  
  
  
