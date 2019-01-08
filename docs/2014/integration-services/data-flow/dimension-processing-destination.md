---
title: 维度处理目标 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimensionprocessingdest.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b8b3e0e7b353ad37aeb3ce87e39bdfc52d2cbcb0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749459"
---
# <a name="dimension-processing-destination"></a>维度处理目标
  维度处理目标加载并处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 维度。 有关维度的详细信息，请参阅[维度（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)。  
  
 维度处理目标包含下列功能：  
  
-   用于执行增量处理、完全处理或更新处理的选项。  
  
-   用于指定维度处理是忽略错误还是在发生指定数量的错误后停止的错误配置。  
  
-   输入列到维度表中列的映射。  
  
 有关处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的详细信息，请参阅[处理选项和设置 (Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>维度处理目标的配置  
 维度处理目标使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器连接到包含目标所处理的维度的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的实例。 有关详细信息，请参阅 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md)。  
  
 此目标有一个输入。 它不支持错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可在 **“维度处理目标编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [维度处理目标编辑器（“连接管理器”页）](../dimension-processing-destination-editor-connection-manager-page.md)  
  
-   [维度处理目标编辑器（“映射”页）](../dimension-processing-destination-editor-mappings-page.md)  
  
-   [维度处理目标编辑器（“高级”页）](../dimension-processing-destination-editor-advanced-page.md)  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](../common-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据流](data-flow.md)   
 [Integration Services 转换](transformations/integration-services-transformations.md)  
  
  
