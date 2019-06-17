---
title: 数据挖掘查询转换 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingquerytrans.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d9ab528b290fdbba841a1a8acf56f1f4f01c8fec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770655"
---
# <a name="data-mining-query-transformation"></a>数据挖掘查询转换
  数据挖掘查询转换针对数据挖掘模型执行预测查询。 此转换包含用于创建数据挖掘扩展 (DMX) 查询的查询生成器。 使用查询生成器可创建自定义语句来使用 DMX 语言针对现有挖掘模型计算转换输入数据。 有关详细信息，请参阅[数据挖掘扩展插件 (DMX) 参考](/sql/dmx/data-mining-extensions-dmx-reference)。  
  
 如果模型是使用同一数据挖掘结构构建的，那么一个转换可以执行多个预测查询。 有关详细信息，请参阅[数据挖掘查询接口](../../../analysis-services/data-mining/data-mining-query-tools.md)。  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>数据挖掘查询转换的配置  
 数据挖掘查询转换使用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 连接管理器来连接包含挖掘结构和挖掘模型的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例。 有关详细信息，请参阅 [Analysis Services Connection Manager](../../connection-manager/analysis-services-connection-manager.md)。  
  
 此转换有一个输入和一个输出。 它不支持错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 **“数据挖掘查询转换编辑器”** 对话框中设置的属性的详细信息，请单击以下主题之一：  
  
-   [数据挖掘查询转换编辑器（“挖掘模型”选项卡）](../../data-mining-query-transformation-editor-mining-model-tab.md)  
  
-   [数据挖掘查询转换编辑器（“挖掘模型”选项卡）](../../data-mining-query-transformation-editor-mining-model-tab.md)  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [转换自定义属性](transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)。  
  
  
