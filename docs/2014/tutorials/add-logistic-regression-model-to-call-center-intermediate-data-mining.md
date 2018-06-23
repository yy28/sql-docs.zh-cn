---
title: 将逻辑回归模型添加到呼叫中心结构 （数据挖掘中级教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 97abb77a-346c-44fa-8959-688dee1af6a8
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ccadf7665b112b6ba1055fdcf69aeb99609c3ab3
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312425"
---
# <a name="adding-a-logistic-regression-model-to-the-call-center-structure-intermediate-data-mining-tutorial"></a>向呼叫中心结构中添加逻辑回归模型（数据挖掘中级教程）
  除了分析可能影响呼叫中心运营的因素之外，您还需要就员工如何提升其服务质量提供一些具体的建议。 在此任务中，您将使用生成探索模型时所使用的挖掘结构，并添加一个用来创建预测的挖掘模型。  
  
 在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中，逻辑回归模型基于神经网络算法，因此可以提供与神经网络模型相同的灵活性和功能， 但更适合于预测二进制结果。  
  
 在此方案中，您将使用用于神经网络模型中的同一挖掘结构。 但是，您将根据自己的业务问题自定义新模型。 您关注提高服务质量并确定需要多少有经验的操作员，因此将设置自己的模型来预测这些值。  
  
 为了确保基于呼叫中心数据的所有模型尽可能类似，将使用与以前相同的种子值。 设置种子参数确保模型从同一起点处理数据并将数据中项目导致的变差最小化。  
  
### <a name="to-add-a-new-mining-model-to-the-call-center-mining-structure"></a>向呼叫中心挖掘结构中添加新的挖掘模型  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，在解决方案资源管理器，右键单击挖掘结构中，**调用 Center 装箱**，然后选择**打开设计器**。  
  
2.  在数据挖掘设计器中，单击**挖掘模型**选项卡。  
  
3.  单击**创建相关的挖掘模型**。  
  
4.  在**新建挖掘模型**对话框中，为**模型名称**，类型`Call Center - LR`。  有关**算法名称**，选择**Microsoft 逻辑回归**。  
  
5.  单击“确定” 。  
  
     新的挖掘模型显示在**挖掘模型**选项卡。  
  
### <a name="to-customize-the-logistic-regression-model"></a>自定义逻辑回归模型  
  
1.  为新的挖掘模型列中`Call Center - LR`，保留事实 CallCenter ID 作为键。  
  
2.  ServiceGrade 和级别到两个运算符的值更改**预测**。  
  
     这些列既可以用作输入，也可以用于预测。 本质上，您对同一数据创建了两个独立的模型：一个预测操作员数，一个预测服务等级。  
  
3.  更改所有其他列调整为**输入**。  
  
### <a name="to-specify-the-seed-and-process-the-models"></a>指定种子并处理模型  
  
1.  在**挖掘模型**选项卡上，右键单击的列，模型命名为调用中心 — LR，然后选择**设置算法参数**。  
  
2.  在为 HOLDOUT_SEED 参数行中，单击下面的空单元格中**值**，和类型`1`。 单击“确定” 。  
  
    > [!NOTE]  
    >  选择哪个值作为种子无关紧要，关键是您需要对所有相关模型使用同一个种子。  
  
3.  在**挖掘模型**菜单上，选择**处理挖掘结构和所有模型**。 单击**是**将更新后的数据挖掘项目部署到服务器。  
  
4.  在**处理挖掘模型**对话框中，单击**运行**。  
  
5.  单击**关闭**关闭**处理进度**对话框中，然后单击**关闭**再次在**处理挖掘模型**对话框。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建 Call Center 模型的预测&#40;中间数据挖掘教程&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [处理要求和注意事项&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  