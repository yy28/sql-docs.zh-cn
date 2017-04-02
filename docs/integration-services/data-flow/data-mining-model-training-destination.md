---
title: "数据挖掘模型定型目标 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.dataminingmodeltrainingdest.f1"
helpviewer_keywords: 
  - "目标 [Integration Services], 数据挖掘模型定型"
  - "数据挖掘模型定型目标"
  - "挖掘模型 [Analysis Services], 定型"
  - "为挖掘模型定型"
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 46
---
# 数据挖掘模型定型目标
  数据挖掘模型定型目标将该目标接收到的数据通过数据挖掘模型算法传递，从而为数据挖掘模型定型。 如果模型是在同一数据结构上生成的，则一个目标可为多个数据挖掘模型定型。 有关详细信息，请参阅 [Mining Structure Columns](../../analysis-services/data-mining/mining-structure-columns.md) 和 [Mining Model Columns](../../analysis-services/data-mining/mining-model-columns.md)。  
  
## 数据挖掘模型定型目标的配置  
 如果目标结构以及在该结构上生成的模型的事例级别列具有内容类型 KEY TIME 或 KEY SEQUENCE，则输入数据必须基于此列排序。 例如，用 Microsoft 时序算法生成的模型使用内容类型 KEY TIME。 如果输入数据未排序，则对模型的处理可能失败。 如果数据需要排序，您可以事先在数据流中使用排序转换对数据进行排序。 此要求不适用于具有 KEY 内容类型的列。 有关详细信息，请参阅[内容类型（数据挖掘）](../../analysis-services/data-mining/content-types-data-mining.md)和[排序转换](../../integration-services/data-flow/transformations/sort-transformation.md)。  
  
> [!NOTE]  
>  数据挖掘模型定型目标的输入必须经过排序。 若要对数据进行排序，您可以将数据挖掘模型定型目标的排序目标上游包括到该数据流中。 有关详细信息，请参阅 [Sort Transformation](../../integration-services/data-flow/transformations/sort-transformation.md)。  
  
 此目标有一个输入，没有输出。  
  
 数据挖掘模型定型目标使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器连接到包含挖掘结构以及目标为其定型的挖掘模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的实例。 有关详细信息，请参阅 [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“数据挖掘模型定型编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [数据挖掘模型定型编辑器（“连接”选项卡）](../../integration-services/data-flow/data-mining-model-training-editor-connection-tab.md)  
  
-   [数据挖掘模型定型编辑器（“列”选项卡）](../../integration-services/data-flow/data-mining-model-training-editor-columns-tab.md)  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../Topic/Common%20Properties.md)  
  
-   [数据挖掘模型定型目标自定义属性](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅[设置数据流组件的属性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
  