---
title: 时序模型查询示例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time series algorithms [Analysis Services]
- MISSING_VALUE_SUBSTITUTION
- time series [Analysis Services]
- predictions [Analysis Services], time series
- EXTEND_MODEL_CASES parameter
- REPLACE_MODEL_CASES parameter
- prediction queries [DMX]
- PREDICTION_SMOOTHING
- content queries [DMX]
ms.assetid: 9a1c527e-2997-493b-ad6a-aaa71260b018
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4098a1b5eade3705e10ab609c47454564a18101d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511415"
---
# <a name="time-series-model-query-examples"></a>时序模型查询示例
  在创建针对数据挖掘模型的查询时，您既可以创建内容查询，也可创建预测查询；内容查询提供有关分析过程中发现的模式的详细信息，而预测查询则使用模型中的模式来对新数据进行预测。 例如，时序模型的内容查询可能提供有关检测到的周期性结构的其他详细信息，而预测查询可能给出接下来 5-10 个时间段的预测。 您还可以使用查询来检索有关模型的元数据。  
  
 本节介绍如何为基于 Microsoft 时序算法的模型创建这两种查询。  
  
 **内容查询**  
  
 [检索模型的周期提示](#bkmk_Query1)  
  
 [检索 ARIMA 模型的公式](#bkmk_Query2)  
  
 [检索 ARTxp 模型的公式](#bkmk_Query3)  
  
 **预测查询**  
  
 [了解何时替换和扩展时序数据](#bkmk_ReplaceExtend)  
  
 [使用 EXTEND_MODEL_CASES 进行预测](#bkmk_EXTEND)  
  
 [使用 REPLACE_MODEL_CASES 进行预测](#bkmk_REPLACE)  
  
 [时序模型中的缺失值替代](#bkmk_MissingValues)  
  
## <a name="getting-information-about-a-time-series-model"></a>获取有关时序模型的信息  
 模型内容查询可以提供有关模型的基本信息，例如创建模型时使用的参数、上次处理模型的时间。 以下示例说明了使用数据挖掘架构行集查询模型内容的基本语法。  
  
###  <a name="bkmk_Query1"></a> 示例查询 1:检索模型的周期提示  
 可通过查询 ARIMA 树或 ARTXP 树检索在时序内找到的周期。 但是，已完成的模型中的周期可能与创建模型时指定为提示的周期不同。 若要检索创建模型时作为参数提供的提示，可以使用以下 DMX 语句来查询挖掘模型内容架构行集：  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 部分结果：  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY = 0.1，MINIMUM_SUPPORT = 10，PERIODICITY_HINT ={1,3}，...|  
  
 默认周期提示为 {1}，将出现在所有模型中；此示例模型是使用可能不在最终模型中出现的附加提示创建的。  
  
> [!NOTE]  
>  此处已将结果截断以提高可读性。  
  
###  <a name="bkmk_Query2"></a> 示例查询 2:检索 ARIMA 模型的公式  
 通过查询单个树中的任何节点，可以检索 ARIMA 模型的公式。 请记住，ARIMA 模型中的每个树都表示不同的周期，如果有多个数据序列，则每个数据序列都将有自己的周期树集。 因此，若要检索特定数据序列的公式，必须先标识树。  
  
 例如，TA 前缀表示该节点是 ARIMA 树的一部分，而 TS 前缀用于 ARTXP 树。 通过查询 NODE_TYPE 值为 27 的节点的模型内容可以找到所有的 ARIMA 根树。 也可以使用 ATTRIBUTE_NAME 值查找特定数据序列的 ARIMA 根节点。 该查询示例查找表示 R250 型号在 Europe 地区销售数量的 ARIMA 节点。  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM Forecasting.CONTENT  
WHERE ATTRIBUTE_NAME = 'R250 Europe: Quantity"  
AND NODE_TYPE = 27  
```  
  
 通过使用该节点 ID，可以检索有关该树的 ARIMA 公式的详细信息。 下面的 DMX 语句检索该数据序列的 ARIMA 公式的缩写形式。 该语句还从嵌套表 NODE_DISTRIBUTION 中检索截获。 在此示例中，通过引用该节点的唯一 ID TA00000007 获取公式。 但是，您需要使用不同的节点 ID，这样您可能会从模型中获得稍有不同的结果。  
  
```  
SELECT FLATTENED NODE_CAPTION as [Short equation],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE   
FROM NODE_DISTRIBUTION) as t  
FROM Forecasting.CONTENT  
WHERE NODE_NAME = 'TA00000007'  
```  
  
 示例结果：  
  
|短公式|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|--------------------|-----------------------|------------------------|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Intercept)|15.24...|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|1|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|12|  
  
 有关如何解释此信息的详细信息，请参阅 [时序模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-time-series-models-analysis-services-data-mining.md)。  
  
###  <a name="bkmk_Query3"></a> 示例查询 3:检索 ARTXP 模型的公式  
 对于 ARTxp 模型，将在树的每个级别存储不同的信息。 有关 ARTxp 模型的结构，以及如何解释公式中的信息的详细信息，请参阅[时序模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-time-series-models-analysis-services-data-mining.md)。  
  
 下面的 DMX 语句检索部分 ARTxp 树的信息，表示 R250 型号在 Europe 的销售数量。  
  
> [!NOTE]  
>  必须将嵌套表列的名称 VARIANCE 括在括号中，以便将它与同名的保留关键字区分开来。 由于嵌套表列 PROBABILITY 和 SUPPORT 在大多数情况下为空，因此这两列不包括在内。  
  
```  
SELECT NODE_CAPTION as [Split information],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
   [VARIANCE]  
   FROM NODE_DISTRIBUTION) AS t  
FROM Forecasting.CONTENT  
WHERE NODE_ATTRIBUTE_NAME = 'R250 Europe:Quantity'  
AND NODE_TYPE = 15  
```  
  
 有关如何解释此信息的详细信息，请参阅 [时序模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-time-series-models-analysis-services-data-mining.md)。  
  
## <a name="creating-predictions-on-a-time-series-model"></a>创建针对时序模型的预测  
 从 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]开始，可以在时序模型中添加新数据并自动将新数据合并到模型中。 您可以通过下列两种方式之一向时序挖掘模型添加新数据：  
  
-   使用 `PREDICTION JOIN` 将外部源中的数据联接到定型数据。  
  
-   使用单独预测查询每次向数据提供一个切片。 有关如何创建单独预测查询的信息，请参阅[数据挖掘查询接口](data-mining-query-tools.md)。  
  
###  <a name="bkmk_ReplaceExtend"></a> 理解替换和扩展操作的行为  
 在时序模型中添加新数据时，可以指定是否扩展或替换定型数据：  
  
-   **扩展：** 在扩展数据序列时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]现有定型数据的结尾处添加新数据。 定型事例的数量也会增加。  
  
     扩展模型事例对于使用新数据持续更新模型很有用。 例如，如果要使定型集随时间增长，则只需扩展该模型。  
  
     若要扩展数据，请在时序模型上创建一个 `PREDICTION JOIN`，指定新数据源，然后使用 `EXTEND_MODEL_CASES` 参数。  
  
-   **将为：** 当替换数据序列中的数据时[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]保留定型的模型，但使用新的数据值替换现有的定型事例的全部或部分。 因此，定型数据的大小永远不会发生变化，但事例本身却可以使用更新的数据不断进行替换。 如果您提供了足够的新数据，则可以使用全新的序列替换定型数据。  
  
     如果您想对一组事例的某个模型定型，然后将该模型应用到不同的数据序列，则替换模型事例非常有用。  
  
     若要替换数据，可以在时序模型上创建一个 `PREDICTION JOIN`，指定新数据源，然后使用 `REPLACE_MODEL_CASES` 参数。  
  
> [!NOTE]  
>  添加新数据时不能进行历史预测。  
  
 无论是扩展还是替换定型数据，始终在结束原始定型集的时间戳处开始预测。 换言之，如果新数据包含 n 个时间段，并且请求对时间步长 1 至 n 进行预测，则预测将与新数据的时间段一致，并且不会获取任何新的预测。  
  
 若要获取对不与新数据重叠的时间段的新预测，必须从新数据序列之后的时间段 n+1 处开始预测，或者确保请求了其他的时间段。  
  
 例如，假定现有模型具有六个月积累的数据。 您想通过添加最近三个月的销售数字来扩展该模型。 同时，您还想对接下来三个月进行预测。 添加新数据时如果只想获得新的预测，则将起点指定为时间段 4，将终点指定为时间段 7。 您可能还要请求全部六个预测，但是，前三个预测的时间段会与刚添加的新数据重叠。  
  
 有关查询示例和使用的语法的详细信息`REPLACE_MODEL_CASES`并`EXTEND_MODEL_CASES`，请参阅[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)。  
  
###  <a name="bkmk_EXTEND"></a> 使用 EXTEND_MODEL_CASES 进行预测  
 根据您是要扩展还是替换模型事例，预测行为会有所不同。 如果要扩展模型，新数据会附加到序列的末尾，并且定型集的大小会增加。 但是，用于预测查询的时间段始终从原始序列的末尾开始。 因此，如果您要添加三个新数据点并请求六个预测，返回的前三个预测将会与新数据重叠。 在这种情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会返回实际的新数据点，而不是进行预测，直到所有新数据点用完为止。 然后， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会根据组合序列进行预测。  
  
 通过这种行为，您可以添加新数据，然后在预测图表中显示实际的销售数字，而不是查看预测。  
  
 例如，若要添加三个新数据点并进行三个新预测，您需要执行下列操作：  
  
-   在时序模型上创建一个 `PREDICTION JOIN`，然后指定三个月新数据的来源。  
  
-   请求六个时间段的预测。 为此，请指定 6 个时间段，其中，起点为时间段 1，终点为时间段 7。 这仅适用于 EXTEND_MODEL_CASES。  
  
-   若要仅获取新预测，请将起点指定为 4，终点指定为 7。  
  
-   您必须使用参数 `EXTEND_MODEL_CASES`。  
  
     将返回前三个时间段的实际销售数字，并返回接下来三个时间段的基于扩展模型的预测。  
  
###  <a name="bkmk_REPLACE"></a> 使用 REPLACE_MODEL_CASES 进行预测  
 在替换模型中的事例时，模型的大小将保持不变，但是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将替换模型中的各个事例。 这对于交叉预测以及需要让定型数据集的大小保持一致的情形很有用。  
  
 例如，您的一个商店的销售数据不足。 您可以对位于特定地区的所有商店的销售量计算平均值，然后定型一个模型，以此来创建一个常规模型。 然后，为了对销售数据不足的商店进行预测，可以仅为该商店创建一个有关新销售数据的 `PREDICTION JOIN`。 在进行此操作时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会保留从地区模型中派生的模式，而使用各个商店的数据替换现有的定型事例。 最后，您的预测值将更为接近各个商店的趋势线。  
  
 使用 `REPLACE_MODEL_CASES` 参数时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会连续将新事例添加到事例集的末尾，并从事例集的开头删除相应数量的事例。 如果您要添加的新数据比原始定型集中的数据多， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将丢弃最早的数据。 如果您提供了足够的新值，则预测可以基于全新的数据。  
  
 例如，假如您已经对包含 1000 行的事例数据集定型了自己的模型。 然后您添加了 100 行新数据。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会从定型集中删除前 100 行，并向该定型集的末尾添加 100 行新数据，总和仍然是 1000 行。 如果您添加了 1100 行新数据，则只使用最新的 1000 行。  
  
 以下是另一个示例。 若要添加新的三个月积累的数据并进行三个新预测，您需要执行下列操作：  
  
-   在时序模型上创建 `PREDICTION JOIN`，并使用 `REPLACE_MODEL_CASE` 参数。  
  
-   指定三个月新数据的来源。 该数据可能来自与原始定型数据完全不同的来源。  
  
-   请求六个时间段的预测。 为此，请指定 6 个时间段，或者将起点指定为时间段 1，终点指定为时间段 7。  
  
    > [!NOTE]  
    >  与 `EXTEND_MODEL_CASES` 不同，您不能返回作为输入数据添加的相同值。 返回的全部六个值都是基于更新模型的预测，其中包括旧数据和新数据。  
  
    > [!NOTE]  
    >  对于 REPLACE_MODEL_CASES，从时间戳 1 开始获取基于新数据的新预测，这会替换旧的定型数据。  
  
 有关查询示例和使用的语法的详细信息`REPLACE_MODEL_CASES`并`EXTEND_MODEL_CASES`，请参阅[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)。  
  
###  <a name="bkmk_MissingValues"></a> 时序模型中的缺失值替代  
 在通过 `PREDICTION JOIN` 语句在时序模型中添加新数据时，新数据集不能有任何缺失值。 如果有任何序列不完整，则该模型必须使用 Null、数值平均值、特定数值平均值或预测值来替换缺失的值。 如果指定了 `EXTEND_MODEL_CASES`，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会将缺失值替换为基于原始模型的预测。 如果您使用`REPLACE_MODEL_CASES`，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]缺失值替换在指定的值*MISSING_VALUE_SUBSTITUTION*参数。  
  
## <a name="list-of-prediction-functions"></a>预测函数的列表  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法均支持一组通用的函数。 但 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序算法支持下表中列出的其他函数。  
  
|||  
|-|-|  
|预测函数|用法|  
|[Lag (DMX)](/sql/dmx/lag-dmx)|返回当前事例的日期与定型集的最近日期之间的若干时间段。<br /><br /> 该函数的一个典型用途是标识最近的定型事例，以使您可以检索有关这些事例的详细数据。|  
|[PredictNodeId (DMX)](/sql/dmx/predictnodeid-dmx)|返回指定的可预测列的节点 ID。<br /><br /> 该函数的一个典型用途是标识生成特定预测值的节点，以使您可以查看与该节点关联的事例，或者检索公式和其他详细信息。|  
|[PredictStdev (DMX)](/sql/dmx/predictstdev-dmx)|返回指定的可预测列中预测的标准偏差。<br /><br /> 该函数取代时序模型不支持的 INCLUDE_STATISTICS 参数。|  
|[PredictVariance (DMX)](/sql/dmx/predictvariance-dmx)|返回指定可预测列的预测方差。<br /><br /> 该函数取代时序模型不支持的 INCLUDE_STATISTICS 参数。|  
|[PredictTimeSeries (DMX)](/sql/dmx/predicttimeseries-dmx)|返回时序的历史预测值或未来预测值。<br /><br /> 还可以通过使用常规预测函数 [Predict (DMX)](/sql/dmx/predict-dmx) 来查询时序模型。|  
  
 有关所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法都支持的通用函数的列表，请参阅[通用预测函数 (DMX)](/sql/dmx/general-prediction-functions-dmx)。 有关特定函数的语法，请参阅[数据挖掘扩展插件 (DMX) 函数引用](/sql/dmx/data-mining-extensions-dmx-function-reference)。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘查询](data-mining-queries.md)   
 [Microsoft 时序算法](microsoft-time-series-algorithm.md)   
 [Microsoft 时序算法技术参考](microsoft-time-series-algorithm-technical-reference.md)   
 [时序模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
