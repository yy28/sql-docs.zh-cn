---
title: 神经网络模型查询示例 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 66f7979dbcf2b547e8f24476f057616c2cd7d3cd
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="neural-network-model-query-examples"></a>神经网络模型查询示例
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在对数据挖掘模型创建查询时，可以创建内容查询，也可以创建预测查询。内容查询提供有关分析时发现的模式的详细信息，预测查询使用模型中的模式来对新数据进行预测。 例如，神经网络模型的内容查询可能会检索模型元数据，如隐藏层数。 而预测查询会基于输入提供分类建议，还可以选择是否提供每个分类的概率。  
  
 本节说明如何为基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法的模型创建查询。  
  
 **内容查询**  
  
 [使用 DMX 获取模型元数据](#bkmk_Query1)  
  
 [从架构行集中检索模型元数据](#bkmk_Query2)  
  
 [示例查询 3：检索模型的输入属性](#bkmk_Query3)  
  
 [示例查询 4：从隐藏层中检索权重](#bkmk_Query4)  
  
 **预测查询**  
  
 [创建单独预测](#bkmk_Query5)  
  
## <a name="finding-information-about-a-neural-network-model"></a>查找有关 Naive Bayes 模型的信息  
 所有挖掘模型都公开算法根据标准化架构（即挖掘模型架构行集）学习的内容。 此信息提供有关模型的详细信息并包含基本元数据、分析中发现的结构以及处理时所使用的参数。 可以使用数据挖掘扩展插件 (DMX) 语句来创建针对该模型内容的查询。  
  
###  <a name="bkmk_Query1"></a> 示例查询 1：使用 DMX 获取模型元数据  
 下面的查询返回与使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法生成的模型有关的一些基本元数据。 在神经网络模型中，模型的父节点仅包含模型的名称、存储模型的数据库的名称以及子节点的数目。 但是，边际统计信息节点 (NODE_TYPE = 24) 会提供这些基本元数据以及与模型中使用的输入列有关的一些派生统计信息。  
  
 以下示例查询基于您在 [数据挖掘中级教程](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b)中创建的、名为 `Call Center Default NN`的挖掘模型。 该模型使用来自呼叫中心的数据来探查人员配备、呼叫次数、订单与问题数之间可能的相关性。 该 DMX 语句检索神经网络模型的边际统计信息节点的数据。 该查询包含 FLATTENED 关键字，因为相关的输入属性统计信息存储在嵌套表 NODE_DISTRIBUTION 中。 但是，如果您的查询访问接口支持分层行集，则无需使用 FLATTENED 关键字。  
  
```  
SELECT FLATTENED MODEL_CATALOG, MODEL_NAME,   
(    SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
     [SUPPORT], [PROBABILITY], VALUETYPE   
     FROM NODE_DISTRIBUTION  
) AS t  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 24  
```  
  
> [!NOTE]  
>  必须将嵌套表列的名称 SUPPORT 和 PROBABILITY 括在方括号中，以便将它们与同名的保留关键字区分开来。  
  
 示例结果：  
  
|MODEL_CATALOG|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|--------------------|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Average Time Per Issue|Missing|0|0|1|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Average Time Per Issue|< 64.7094100096|11|0.407407407|5|  
  
 有关架构行集中的列在神经网络模型的上下文中的含义的定义，请参阅 [神经网络模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)的挖掘模型。  
  
###  <a name="bkmk_Query2"></a> 示例查询 2：从架构行集中检索模型元数据  
 通过查询数据挖掘架构行集，可以找到在 DMX 内容查询中返回的相同信息。 但是，架构行集还提供一些额外的列。 下面的示例查询返回模型的创建日期、修改日期以及上次处理模型日期。 该查询还返回可预测列（这从模型内容中并不能轻易获得）以及用于生成该模型的参数。 此信息对于模型的归档很有用。  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center Default NN'  
```  
  
 示例结果：  
  
|||  
|-|-|  
|MODEL_NAME|Call Center Default NN|  
|DATE_CREATED|1/10/2008 5:07:38 PM|  
|LAST_PROCESSED|1/10/2008 5:24:02 PM|  
|PREDICTION_ENTITY|Average Time Per Issue,<br /><br /> Grade Of Service,<br /><br /> Number Of Orders|  
|MINING_PARAMETERS|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=0,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100, SAMPLE_SIZE=10000, HIDDEN_NODE_RATIO=4|  
  
###  <a name="bkmk_Query3"></a> 示例查询 3：检索模型的输入属性  
 通过查询输入层 (NODE_TYPE = 18) 的子节点 (NODE_TYPE = 20) 可以检索用于创建模型的输入属性值对。 下面的查询从节点说明返回输入属性列表。  
  
```  
SELECT NODE_DESCRIPTION  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 示例结果：  
  
|NODE_DESCRIPTION|  
|-----------------------|  
|Average Time Per Issue=64.7094100096 - 77.4002099712|  
|Day Of Week=Fri.|  
|Level 1 Operators|  
  
 此处仅显示结果中一些具有代表性的行。 但是，可以看到 NODE_DESCRIPTION 提供了因输入属性的数据类型不同而略有差异的信息。  
  
-   如果输入属性为离散值或离散化的值，则会返回该属性及其值或其离散化范围。  
  
-   如果输入属性为连续数值数据类型，则 NODE_DESCRIPTION 仅包含属性名称。 但是，可以检索嵌套的 NODE_DISTRIBUTION 表以获取平均值，或者返回 NODE_RULE 以获取数值范围的最小值和最大值。  
  
 下面的查询显示如何查询嵌套的 NODE_DISTRIBUTION 表以在一列中返回属性，并在另一列中返回这些属性的值。 对于连续属性，属性值由其平均值来代表。  
  
```  
SELECT FLATTENED   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE  
FROM NODE_DISTRIBUTION) as t  
FROM [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 21  
```  
  
 示例结果：  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|-----------------------|------------------------|  
|Average Time Per Issue|64.7094100096 - 77.4002099712|  
|Day Of Week|Fri.|  
|Level 1 Operators|3.2962962962963|  
  
 最小和最大范围值存储在 NODE_RULE 列中，并表示为 XML 片段，如下例所示：  
  
```  
<NormContinuous field="Level 1 Operators">    
  <LinearNorm orig="2.83967303681711" norm="-1" />    
  <LinearNorm orig="3.75291955577548" norm="1" />    
</NormContinuous>    
```  
  
###  <a name="bkmk_Query4"></a> 示例查询 4：从隐藏层中检索权重  
 神经网络模型的模型内容采用特定的结构，以便轻松检索网络中的任何节点的详细信息。 此外，节点的 ID 号提供了有助于您标识节点类型之间关系的信息。  
  
 下面的查询演示了如何检索隐藏层特定节点下存储的系数。 该隐藏层包含一个组织程序节点 (NODE_TYPE = 19) 和多个子节点 (NODE_TYPE = 22)，组织程序节点仅包含元数据，子节点包含属性和值的各种组合的系数。 此查询仅返回系数节点。  
  
```  
SELECT FLATTENED TOP 1 NODE_UNIQUE_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM  [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 22  
AND [PARENT_UNIQUE_NAME] = '40000000200000000' FROM [Call Center Default NN].CONTENT  
```  
  
 示例结果：  
  
|NODE_UNIQUE_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|------------------------|-----------------------|------------------------|-----------------|  
|70000000200000000|6000000000000000a|-0.178616518|7|  
|70000000200000000|6000000000000000b|-0.267561918|7|  
|70000000200000000|6000000000000000c|0.11069497|7|  
|70000000200000000|6000000000000000d|0.123757712|7|  
|70000000200000000|6000000000000000e|0.294565343|7|  
|70000000200000000|6000000000000000f|0.22245318|7|  
|70000000200000000||0.188805045|7|  
  
 此处显示的部分结果说明了神经网络模型内容如何将隐藏节点与输入节点相关联。  
  
-   隐藏层中节点的唯一名称始终以 70000000 开头。  
  
-   输入层中节点的唯一名称始终以 60000000 开头。  
  
 因此，这些结果显示由 ID 70000000200000000 表示的节点可使六个不同的系数 (VALUETYPE = 7) 传递给它。 系数的值在 ATTRIBUTE_VALUE 列中。 您可以使用 ATTRIBUTE_NAME 列中的节点 ID 来明确地确定系数对应哪一个输入属性。 例如，节点 ID 6000000000000000a 对应输入属性和值 `Day of Week = 'Tue.'` 。您可以使用节点 ID 来创建一个查询，或者可以使用 [Microsoft 一般内容树查看器](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)浏览到该节点。  
  
 同样，如果您查询输出层 (NODE_TYPE = 23) 中各节点的 NODE_DISTRIBUTION 表，则会看到每个输出值的系数。 但是，在输出层中，指针将回指隐藏层的节点。 有关详细信息，请参阅 [神经网络模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)的挖掘模型。  
  
## <a name="using-a-neural-network-model-to-make-predictions"></a>使用神经网络模型进行预测  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法支持分类和回归。 您可以对这些模型使用预测函数来提供新数据并创建单独预测或批预测。  
  
###  <a name="bkmk_Query5"></a> 示例查询 5：创建单独预测  
 对神经网络模型生成预测查询的最简单方法是使用预测查询生成器，在 **和** 的数据挖掘设计器的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] “挖掘预测” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡中都提供了该生成器。 您可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络查看器中浏览模型来筛选感兴趣的属性并查看趋势，然后切换到 **“挖掘预测”** 选项卡来创建一个查询并预测那些趋势的新值。  
  
 例如，您可以浏览呼叫中心模型来查看订单量和其他属性之间的相关性。 若要执行此操作，打开模型查看器中，在中，对于**输入**，选择**\<所有 >**。  接下来，为 **“输出”**选择 **“订单数”**。 对于 **“值 1”**，请选择表示最多订单的范围，对于 **“值 2”**，请选择表示最少订单的范围。 然后您将对模型将其与订单量关联的所有属性一目了然。  
  
 通过浏览查看器中的结果，您将发现一周中的某些天订单量较少，而操作员数的增加似乎与较高的销售额相关联。 然后您可以使用针对模型的预测查询来测试假设情况，询问在订单量少的日子增加级别 2 操作员的人数是否能增加订单量。 为此，请创建如下所示的查询：  
  
```  
SELECT Predict([Call Center Default NN].[Number of Orders]) AS [Predicted Orders],  
PredictProbability([Call Center Default NN].[Number of Orders]) AS [Probability]  
FROM [Call Center Default NN]  
NATURAL PREDICTION JOIN   
(SELECT 'Tue.' AS [Day of Week],  
13 AS [Level 2 Operators]) AS t  
```  
  
 示例结果：  
  
|Predicted Orders|概率|  
|----------------------|-----------------|  
|364|0.9532…|  
  
 预测的周二销售量高于当前销售范围，并且该预测的概率非常高。 但是，您可能要使用批处理创建多个预测来测试对模型的各种假设。  
  
> [!NOTE]  
>  Excel 2007 数据挖掘外接程序提供的逻辑回归向导很容易回答一些复杂问题，如针对一个特定班次，要将服务等级提高到目标级别，需要多少名二级操作员。 数据挖掘外接程序是免费下载的，并包含基于神经网络和/或逻辑回归算法的向导。 有关详细信息，请参阅 [Data Mining Add-ins for Office 2007](http://go.microsoft.com/fwlink/?LinkID=117790) （Office 2007 数据挖掘外接程序）网站。  
  
## <a name="list-of-prediction-functions"></a>预测函数的列表  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法均支持一组通用的函数。 没有特定于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法的预测函数；但该算法支持下表中列出的函数。  
  
|||  
|-|-|  
|预测函数|用法|  
|[IsDescendant & #40; DMX & #41;](../../dmx/isdescendant-dmx.md)|确定一个节点是否是神经网络图中另一个节点的子节点。|  
|[PredictAdjustedProbability & #40; DMX & #41;](../../dmx/predictadjustedprobability-dmx.md)|返回加权的概率。|  
|[PredictHistogram & #40; DMX & #41;](../../dmx/predicthistogram-dmx.md)|返回与当前预测值相关的值的表。|  
|[PredictVariance (DMX)](../../dmx/predictvariance-dmx.md)|返回预测值的方差。|  
|[PredictProbability & #40; DMX & #41;](../../dmx/predictprobability-dmx.md)|返回预测值的概率。|  
|[PredictStdev & #40; DMX & #41;](../../dmx/predictstdev-dmx.md)|返回预测值的标准偏差。|  
|[PredictSupport & #40; DMX & #41;](../../dmx/predictsupport-dmx.md)|对于神经网络模型和逻辑回归模型，该函数将返回表示整个模型的定型集大小的单个值。|  
  
 有关对所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法都通用的函数列表，请参阅[算法参考（Analysis Services - 数据挖掘）](https://technet.microsoft.com/library/bb895228\(v=sql.105\).aspx)。 有关特定函数的语法，请参阅[数据挖掘扩展插件 (DMX) 函数引用](../../dmx/data-mining-extensions-dmx-function-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 神经网络算法](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Microsoft 神经网络算法技术参考](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [神经网络模型 & #40; 的挖掘模型内容Analysis Services-数据挖掘 & #41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [第 5 课： 生成神经网络和逻辑回归模型 & #40; 数据挖掘中级教程 & #41;](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b)  
  
  
