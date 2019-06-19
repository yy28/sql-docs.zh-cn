---
title: 向呼叫中心结构 （数据挖掘中级教程） 中添加逻辑回归模型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 97abb77a-346c-44fa-8959-688dee1af6a8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 32e66a84dea20964c11c7de0aa568530aa8c28c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62823274"
---
# <a name="adding-a-logistic-regression-model-to-the-call-center-structure-intermediate-data-mining-tutorial"></a>向呼叫中心结构中添加逻辑回归模型（数据挖掘中级教程）
  除了分析可能影响呼叫中心运营的因素之外，您还需要就员工如何提升其服务质量提供一些具体的建议。 在此任务中，您将使用生成探索模型时所使用的挖掘结构，并添加一个用来创建预测的挖掘模型。  
  
 在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中，逻辑回归模型基于神经网络算法，因此可以提供与神经网络模型相同的灵活性和功能， 但更适合于预测二进制结果。  
  
 在此方案中，您将使用用于神经网络模型中的同一挖掘结构。 但是，您将根据自己的业务问题自定义新模型。 您关注提高服务质量并确定需要多少有经验的操作员，因此将设置自己的模型来预测这些值。  
  
 为了确保基于呼叫中心数据的所有模型尽可能类似，将使用与以前相同的种子值。 设置种子参数确保模型从同一起点处理数据并将数据中项目导致的变差最小化。  
  
### <a name="to-add-a-new-mining-model-to-the-call-center-mining-structure"></a>向呼叫中心挖掘结构中添加新的挖掘模型  
  
1.  在中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，在解决方案资源管理器中右键单击挖掘结构**Call Center Binned**，然后选择**打开设计器**。  
  
2.  在数据挖掘设计器中，单击**挖掘模型**选项卡。  
  
3.  单击**创建相关的挖掘模型**。  
  
4.  在中**新建挖掘模型**对话框中，对于**模型名称**，类型`Call Center - LR`。  有关**算法名称**，选择**Microsoft 逻辑回归**。  
  
5.  单击“确定”  。  
  
     新的挖掘模型将显示在**挖掘模型**选项卡。  
  
### <a name="to-customize-the-logistic-regression-model"></a>自定义逻辑回归模型  
  
1.  为新挖掘模型列中`Call Center - LR`，将 Fact CallCenter ID 作为键。  
  
2.  将 ServiceGrade 和 Level Two Operators 到的值更改**Predict**。  
  
     这些列既可以用作输入，也可以用于预测。 本质上，您对同一数据创建了两个独立的模型：一个预测操作员数，一个预测服务等级。  
  
3.  更改到的所有其他列**输入**。  
  
### <a name="to-specify-the-seed-and-process-the-models"></a>指定种子并处理模型  
  
1.  在中**挖掘模型**选项卡上，该模型名为 Call Center-LR，右键单击该列并选择**设置算法参数**。  
  
2.  在 HOLDOUT_SEED 参数所在的行，单击下的空单元格**值**，然后键入`1`。 单击“确定”  。  
  
    > [!NOTE]  
    >  选择哪个值作为种子无关紧要，关键是您需要对所有相关模型使用同一个种子。  
  
3.  在中**挖掘模型**菜单中，选择**处理挖掘结构和所有模型**。 单击**是**将更新后的数据挖掘项目部署到服务器。  
  
4.  在中**处理挖掘模型**对话框中，单击**运行**。  
  
5.  单击**关闭**以关闭**处理进度**对话框中，然后单击**关闭**中再次**处理挖掘模型**对话框。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建呼叫中心模型的预测&#40;数据挖掘中级教程&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [处理要求和注意事项（数据挖掘）](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
