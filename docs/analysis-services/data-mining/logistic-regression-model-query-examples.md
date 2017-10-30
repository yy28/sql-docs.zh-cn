---
title: "逻辑回归模型查询示例 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logistic regression [Analysis Services]
- content queries [DMX]
ms.assetid: 7c8e13a3-5c67-46c2-abfa-4881e6ef9c62
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b329e0883ef165a01577cd536a8030640c99d2e7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="logistic-regression-model-query-examples"></a>逻辑回归模型查询示例
  在对数据挖掘模型创建查询时，可以创建内容查询，也可以创建预测查询。内容查询提供有关分析时发现的模式的详细信息，预测查询使用模型中的模式来应用新数据进行预测。  
  
 本节介绍如何为基于 Microsoft 逻辑回归算法的模型创建查询。  
  
 **内容查询**  
  
 [使用数据挖掘架构行集检索模型参数](#bkmk_Query1)  
  
 [使用 DMX 查找有关模型的其他详细信息](#bkmk_Query2)  
  
 **预测查询**  
  
 [对连续值进行预测](#bkmk_Query3)  
  
 [对离散值进行预测](#bkmk_Query4)  
  
##  <a name="bkmk_top"></a> 获取有关逻辑回归模型的信息  
 逻辑回归模型是使用带有一组特殊参数的 Microsoft 神经网络算法创建的；因此，逻辑回归模型具有某些与神经网络模型相同的信息，但是会简单些。 若要了解模型内容的结构以及哪些节点存储哪类信息，请参阅 [逻辑回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)。  
  
 若要继续探讨查询方案，可以按“数据挖掘中级教程”中的下一节所述，创建逻辑回归模型： [第 5 课：生成神经网络模型和逻辑回归模型（数据挖掘中级教程）](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b)。  
  
 此外，还可以使用 [数据挖掘基础教程](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)中的挖掘结构 Targeted Mailing。  
  
```  
ALTER MINING STRUCTURE [Targeted Mailing]  
ADD MINING MODEL [TM_Logistic Regression]  
([Customer Key],  
[Age],  
[Bike Buyer] PREDICT,  
[Yearly Income] PREDICT,  
[Commute Distance],  
[English Education],  
Gender,  
[House Owner Flag],  
[Marital Status],  
[Number Cars Owned],  
[Number Children At Home],  
[Region],  
[Total Children]  
)  
USING Microsoft_Logistic_Regression  
```  
  
###  <a name="bkmk_Query1"></a> 示例查询 1：使用数据挖掘架构行集检索模型参数  
 通过查询数据挖掘架构行集，您可以找到有关模型的元数据，如模型创建时间、上次处理模型的时间、模型基于的挖掘结构的名称以及用作可预测属性的列的名称。 下面的示例返回首次创建模型时所用的参数、模型的名称和类型以及模型的创建时间。  
  
```  
SELECT MODEL_NAME, SERVICE_NAME, DATE_CREATED, MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center_LR'  
```  
  
 示例结果：  
  
|MODEL_NAME|SERVICE_NAME|DATE_CREATED|MINING_PARAMETERS|  
|-----------------|-------------------|-------------------|------------------------|  
|Call Center_LR|Microsoft_Logistic_Regression|04/07/2009 20:38:33|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=1, MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255, MAXIMUM_STATES=100, SAMPLE_SIZE=10000|  
  
###  <a name="bkmk_Query2"></a> 示例查询 2：使用 DMX 查找有关模型的其他详细信息  
 下面的查询返回有关逻辑回归模型的一些基本信息。 逻辑回归模型在很多方面与神经网络模型类似，包括都存在描述用作输入的值的边际统计信息节点 (NODE_TYPE = 24)。 此示例查询使用 Targeted Mailing 模型，并通过从嵌套表 NODE_DISTRIBUTION 中检索所有输入的值来获取这些值。  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM [TM_Logistic Regression].CONTENT   
```  
  
 部分结果：  
  
|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|年龄|缺少|0|0|0|1|  
|年龄|45.43491192|17484|1|126.9544114|3|  
|Bike Buyer|缺少|0|0|0|1|  
|Bike Buyer|0|8869|0.507263784|0|4|  
|Bike Buyer|1|8615|0.492736216|0|4|  
|上下班路程|缺少|0|0|0|1|  
|上下班路程|5-10 英里|3033|0.173472889|0|4|  
  
 实际查询会返回多得多的行；但是此示例演示了所提供的有关输入的信息类型。 对于离散输入，每个可能值都列在表中。 对于“年龄”之类的连续值输入，全部列出是不可能的，所以输入被离散化为均值。 有关如何使用边际统计信息节点中的信息的详细信息，请参阅 [逻辑回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)。  
  
> [!NOTE]  
>  为便于查看，结果是平展的，但是，如果您的访问接口支持分层行集，则可在单个列中返回嵌套表。  
  
## <a name="prediction-queries-on-a-logistic-regression-model"></a>针对逻辑回归模型的预测查询  
 对每种挖掘模型都可以使用 [Predict (DMX)](../../dmx/predict-dmx.md) 函数向模型提供新数据并基于新值进行预测。 还可以使用函数返回有关预测的其他信息，例如，预测正确性的概率。 本节提供针对逻辑回归模型的预测查询的一些示例。  
  
###  <a name="bkmk_Query3"></a> 示例查询 3：对连续值进行预测  
 由于逻辑回归支持在输入和预测中都使用连续属性，因此可以轻松地在您的数据中创建与各种因素相关的模型。 您可以使用预测查询来探查这些因素之间的关系。  
  
 以下查询示例基于中级教程中的 Call Center（呼叫中心）模型，并创建了预测 Friday AM shift（周五早班）的服务等级的单独查询。 [PredictHistogram (DMX)](../../dmx/predicthistogram-dmx.md) 函数返回一个嵌套表，该表提供与用于了解预测值的有效性相关的统计信息。  
  
```  
SELECT  
  Predict([Call Center_LR].[Service Grade]) as Predicted ServiceGrade,  
  PredictHistogram([Call Center_LR].[Service Grade]) as [Results],  
FROM  
  [Call Center_LR]  
NATURAL PREDICTION JOIN  
(SELECT 'Friday' AS [Day Of Week],  
  'AM' AS [Shift]) AS t  
```  
  
 示例结果：  
  
|预测服务等级|Service Grade|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-----------------------------|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.102601830123659|0.102601830123659|83.0232558139535|0.988372093023256|0|0.00120552660600087|0.034720694203902|  
|||0.976744186046512|0.0116279069767442|0.0116279069767442|0|0|  
  
 有关嵌套表 NODE_DISTRIBUTION 中的概率、支持和标准偏差值的详细信息，请参阅 [逻辑回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)。  
  
###  <a name="bkmk_Query4"></a> 示例查询 4：对离散值进行预测  
 要分析产生二进制结果的因素时通常使用逻辑回归。 尽管教程中使用的模型预测的是连续值 **ServiceGrade**，但实际生活中你可能还是希望设置该模型来预测服务等级是否符合特定的离散化目标值。 或者，您可以使用连续值来输出预测，但之后将这些预测结果分组到 **较好**、 **一般**或 **较差**这几个等级中。  
  
 下面的示例演示如何更改可预测属性的分组方式。 若要执行此操作，您需要复制挖掘结构，然后更改目标列的离散化方法，以便值归入各分组而不是连续的。  
  
 以下过程介绍如何更改呼叫中心数据中的 Service Grade 值的分组。  
  
##### <a name="to-create-a-discretized-version-of-the-call-center-mining-structure-and-models"></a>创建 Call Center 挖掘结构和模型的离散化版本  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的解决方案资源管理器中，展开 **“挖掘结构”**。  
  
2.  右键单击 Call Center.dmm 并选择“复制”。  
  
3.  右键单击 **“挖掘结构”** ，然后选择 **“粘贴”**。 将添加名为 Call Center 1 的新挖掘结构。  
  
4.  右键单击新的挖掘结构，然后选择“重命名”。 键入新名称 **Call Center Discretized**。  
  
5.  双击新的挖掘结构以在设计器中将其打开。 请注意，随之复制了所有挖掘模型，并且都具有扩展名 1。 暂时将这些名称保留原样。  
  
6.  在“挖掘结构”选项卡中，右键单击 Service Grade 对应的列，然后选择“属性”。  
  
7.  将 **Content** 属性从 **“连续”** 更改为 **“离散化”**。 将 **DiscretizationMethod** 属性更改为 **“分类”**。 对于 Discretization BucketCount，键入 **3**。  
  
    > [!NOTE]  
    >  这些参数仅用于演示过程，不一定生成有效模型。  
  
8.  从 **“挖掘模型”** 菜单上选择 **“处理挖掘结构和所有模型”**。  
  
 以下示例查询基于此离散化模型，并预测了周中某指定日期的服务等级以及每个预测的结果的概率。  
  
```  
SELECT  
  (PredictHistogram([Call Center_LR 1].[Service Grade])) as [Predictions]  
FROM  
  [Call Center_LR 1]  
NATURAL PREDICTION JOIN  
(SELECT 'Saturday' AS [Day Of Week]) AS t    
```  
  
 预期的结果：  
  
 **预测：**  
  
|Service Grade|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.10872718383125|35.7246504770641|0.425293458060287|0.0170168360030293|0|0|  
|0.05855769230625|31.7098880800703|0.377498667619885|0.020882020060454|0|0|  
|0.170169491525|15.6109159883202|0.185844237956192|0.0661386571386049|0|0|  
||0.954545454545455|0.0113636363636364|0.0113636363636364|0|0|  
  
 请注意，预测结果已分组到指定的三个类别中；但是，这些分组基于数据中实际值的分类，而不是基于您可能设置为业务目标的任意值。  
  
## <a name="list-of-prediction-functions"></a>预测函数的列表  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法均支持一组通用的函数。 但 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 逻辑回归算法还额外支持下表中列出的函数。  
  
|||  
|-|-|  
|预测函数|用法|  
|[IsDescendant (DMX)](../../dmx/isdescendant-dmx.md)|确定一个节点是否是模型中另一个节点的子节点。|  
|[PredictAdjustedProbability (DMX)](../../dmx/predictadjustedprobability-dmx.md)|返回指定状态调整后的概率。|  
|[PredictHistogram (DMX)](../../dmx/predicthistogram-dmx.md)|返回指定列的一个预测值或一组值。|  
|[PredictProbability (DMX)](../../dmx/predictprobability-dmx.md)|返回指定状态的概率。|  
|[PredictStdev (DMX)](../../dmx/predictstdev-dmx.md)|返回预测值的标准偏差。|  
|[PredictSupport (DMX)](../../dmx/predictsupport-dmx.md)|返回指定状态的支持值。|  
|[PredictVariance (DMX)](../../dmx/predictvariance-dmx.md)|返回指定列的方差。|  
  
 有关所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法都支持的通用函数的列表，请参阅[通用预测函数 (DMX)](../../dmx/general-prediction-functions-dmx.md)。 有关特定函数的语法，请参阅[数据挖掘扩展插件 (DMX) 函数引用](../../dmx/data-mining-extensions-dmx-function-reference.md)。  
  
> [!NOTE]  
>  对于神经网络模型和逻辑回归模型，[PredictSupport (DMX)](../../dmx/predictsupport-dmx.md) 函数将返回表示整个模型的定型集大小的单个值。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft 逻辑回归算法](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)   
 [Microsoft 逻辑回归算法技术参考](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)   
 [逻辑回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)   
 [第 5 课： 生成神经网络和逻辑回归模型 &#40; 数据挖掘中级教程 &#41;](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b)  
  
  

