---
title: 分区处理目标 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partitionprocessingdest.f1
helpviewer_keywords:
- partitions [Analysis Services], processing
- Partition Processing destination [Integration Services]
- destinations [Integration Services], Partition Processing
ms.assetid: 36c592ff-3f78-4a58-b496-31c1c8eee131
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 53ef09d19b62c0e6ce7742c41581d3cdefdfc374
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68890554"
---
# <a name="partition-processing-destination"></a>分区处理目标
  分区处理目标加载并处理[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]分区。 有关分区的详细信息，请参阅[分区（Analysis Services - 多维数据）](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data)。  
  
 分区处理目标包含下列功能：  
  
-   用于执行增量处理、完全处理或更新处理的选项。  
  
-   用于指定处理是忽略错误，还是在发生指定数量的错误后停止的错误配置。  
  
-   输入列到分区列的映射。  
  
 有关处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的详细信息，请参阅[处理选项和设置 (Analysis Services)](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services)。  
  
> [!NOTE]  
>  此处所述的任何不适用于 Analysis Services 表格模型。  你无法将输入列映射到表格模型的分区列。 您可以改用 [Analysis Services Execute DDL Task](../control-flow/analysis-services-execute-ddl-task.md) 处理分区。  
  
## <a name="configuration-of-the-partition-processing-destination"></a>分区处理目标的配置  
 分区处理目标使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或包含目标所处理的多维数据集和分区的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。 有关详细信息，请参阅 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md)。  
  
 此目标有一个输入。 它不支持错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 **“分区处理目标编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [分区处理目标编辑器 &#40;连接管理器页&#41;](../partition-processing-destination-editor-connection-manager-page.md)  
  
-   [分区处理目标编辑器 &#40;映射 "页面&#41;](../partition-processing-destination-editor-mappings-page.md)  
  
-   [分区处理目标编辑器 &#40;高级页面&#41;](../partition-processing-destination-editor-advanced-page.md)  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](../common-properties.md)  
  
-   [分区处理目标自定义属性](partition-processing-destination-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](set-the-properties-of-a-data-flow-component.md)。  
  
  
