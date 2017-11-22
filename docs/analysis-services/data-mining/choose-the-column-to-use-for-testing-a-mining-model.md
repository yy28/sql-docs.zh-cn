---
title: "选择用于测试挖掘模型列 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [data mining], predictable mining columns
- Mining Accuracy Chart [Analysis Services], columns
- predictable mining columns [Analysis Services]
ms.assetid: c6a8f23a-da21-4f31-9521-99460d624649
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b5b70b350d54987869c77ced1cebfbd8f7b00ec1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="choose-the-column-to-use-for-testing-a-mining-model"></a>选择用于测试挖掘模型的列
  您必须决定要访问哪个结果才能度量挖掘模型的准确性。 大多数数据挖掘模型都要求您在创建模型时至少选择一列用作可预测属性。 因此，在测试模型准确性时，您一般必须选择要测试的属性。  
  
 下表介绍了选择在测试中使用的可预测属性时应注意的一些其他事项：  
  
-   某些类型的数据挖掘模型（如神经网络，它能浏览很多属性之间的关系）可以预测多个属性。  
  
-   其他类型的挖掘模型（如聚类分析模型）不必具有可预测属性。 除非聚类分析模型具有可预测属性，否则无法测试它们。  
  
-   若要创建散点图或度量回归模型的准确性，则需选择连续可预测属性作为结果。 在这种情况下，您不能指定目标值。 如果要创建散点图之外的任何内容，则基础挖掘结构列的内容类型还必须为 **“离散”** 或 **“离散化”**。  
  
-   如果选择离散属性作为可预测结果，则还可以指定一个目标值，或者可以将 **“预测值”** 字段留空。 如果包括 **“预测值”**，则图表将只度量模型预测目标值的有效性。 如果不指定目标结果，则会度量模型预测所有结果的准确性。  
  
-   如果要在一个准确性图表中包含多个模型并对它们进行比较，则所有模型都必须使用相同的可预测列。  
  
-   在创建交叉验证报表时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将自动分析所有具有相同可预测属性的模型。  
  
-   当选择了选项 **“同步预测列和值”**时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会自动选择具有相同名称和匹配的数据类型的可预测列。 如果您的列不满足这些条件，则可以关闭此选项并手动选择一个可预测列。 如果要使用具有与该模型不同的列的外部数据集测试该模型，则可能需要执行此操作。 但是，如果您选择的列的数据类型有误，则您将收到错误或错误的结果。  
  
### <a name="specify-the-outcome-to-predict"></a>指定要预测的结果  
  
1.  双击挖掘结构以在数据挖掘设计器中将其打开。  
  
2.  选择 **“挖掘准确性图表”** 选项卡。  
  
3.  选择 **“输入选择”** 选项卡。  
  
4.  在 **“输入选择”** 选项卡的 **“可预测列名称”**下，为要包含在图表中的每个模型选择一个可预测列。  
  
     **“可预测列名称”** 框中提供的挖掘模型列只有使用类型设置为 **“预测”** 或 **“仅预测”**的列。  
  
5.  如果希望确定模型的提升情况，则必须从 **“预测值”** 列表为该模型选择要度量的特定结果值。  
  
## <a name="see-also"></a>另请参阅  
 [选择和映射模型测试数据](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)   
 [选择准确性图表类型和设置图表选项](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  
