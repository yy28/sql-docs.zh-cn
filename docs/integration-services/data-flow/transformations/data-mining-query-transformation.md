---
title: "数据挖掘查询转换 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataminingquerytrans.f1
- sql13.dts.designer.dmquerytransformation.miningmodel.f1
- sql13.dts.designer.dmquerytransformation.query.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: 7ec5d0d1168e49fb38ce8b58eaa75d6c0d6c51b5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/19/2017

---
# <a name="data-mining-query-transformation"></a>数据挖掘查询转换
  数据挖掘查询转换针对数据挖掘模型执行预测查询。 此转换包含用于创建数据挖掘扩展 (DMX) 查询的查询生成器。 使用查询生成器可创建自定义语句来使用 DMX 语言针对现有挖掘模型计算转换输入数据。 有关详细信息，请参阅[数据挖掘扩展插件 (DMX) 参考](../../../dmx/data-mining-extensions-dmx-reference.md)。  
  
 如果模型是使用同一数据挖掘结构构建的，那么一个转换可以执行多个预测查询。 有关详细信息，请参阅 [数据挖掘查询工具](../../../analysis-services/data-mining/data-mining-query-tools.md)。  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>数据挖掘查询转换的配置  
 数据挖掘查询转换使用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 连接管理器来连接包含挖掘结构和挖掘模型的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例。 有关详细信息，请参阅 [Analysis Services Connection Manager](../../../integration-services/connection-manager/analysis-services-connection-manager.md)。  
  
 此转换有一个输入和一个输出。 它不支持错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [转换自定义属性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="data-mining-query-transformation-editor-mining-model-tab"></a>数据挖掘查询转换编辑器（“挖掘模型”选项卡）
  可以使用 **“数据挖掘查询转换编辑器”** 对话框的 **“挖掘模型”** 选项卡选择数据挖掘结构及其挖掘模型。  
  
### <a name="options"></a>选项  
 **连接**  
 使用列表框选择现有 Analysis Services 连接，或使用下面介绍的“新建”按钮创建新的连接。  
  
 **新建**  
 通过使用“添加 Analysis Services 连接管理器”对话框创建一个新连接。  
  
 **挖掘结构**  
 从可用挖掘模型结构的列表中进行选择。  
  
 **挖掘模型**  
 查看与所选数据挖掘结构关联的挖掘模型的列表。  
  
## <a name="data-mining-query-transformation-editor-query-tab"></a>数据挖掘查询转换编辑器（“查询”选项卡）
  可以使用 **“数据挖掘查询转换编辑器”** 对话框的 **“查询”** 选项卡创建预测查询。  
  
### <a name="options"></a>选项  
 **数据挖掘查询**  
 将数据挖掘扩展插件 (DMX) 查询直接键入文本框中。  
  
 **生成新查询**  
 单击“生成新查询”可以通过使用图形查询生成器来创建数据挖掘扩展插件 (DMX) 查询。  
  

