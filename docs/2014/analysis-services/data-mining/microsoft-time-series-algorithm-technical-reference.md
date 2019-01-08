---
title: Microsoft 时序算法技术参考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ARTXP
- HISTORICAL_MODEL_GAP parameter
- AUTO_DETECT_PERIODICITY parameter
- time series algorithms [Analysis Services]
- ARIMA
- INSTABILITY_SENSITIVITY parameter
- PERIODICITY_HINT parameter
- MAXIMUM_SERIES_VALUE parameter
- time series [Analysis Services]
- MINIMUM_SUPPORT parameter
- HISTORIC_MODEL_COUNT parameter
- FORECAST_METHOD parameter
- MISSING_VALUE_SUBSTITUTION parameter
- MINIMUM_SERIES_VALUE parameter
- COMPLEXITY_PENALTY parameter
- PREDICTION_SMOOTHING parameter
ms.assetid: 7ab203fa-b044-47e8-b485-c8e59c091271
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 04183bb7e6376d1a22bfbf0882388e15940cf4da
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53350708"
---
# <a name="microsoft-time-series-algorithm-technical-reference"></a>Microsoft Time Series Algorithm Technical Reference
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序算法包括两个用于分析时序的独立的算法：  
  
-   ARTXP 算法是在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中引入的，针对预测序列中的下一个可能值进行了优化。  
  
-   ARIMA 算法是在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中添加的，用于提高长期预测的准确性。  
  
 默认情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 分别使用每个算法给模型定型，然后结合结果为数目可变的预测产生最佳预测。 也可以基于您的数据和预测要求选择仅使用其中的一个算法。 在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]中，还可以自定义用于在预测过程中控制算法混合的截止点。  
  
 本主题提供以下方面的附加信息：每个算法的实现原理，以及可以如何通过设置参数来微调分析和预测结果对算法进行自定义。  
  
## <a name="implementation-of-the-microsoft-time-series-algorithm"></a>Microsoft 时序算法的实现  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 研究院开发了在 SQL Server 2005 中使用的原始 ARTXP 算法，并且将该实现基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法。 因此，该 ARTXP 算法可描述为用于表示周期性时序数据的自动回归树模型。 此算法将数目可变的过去项与要预测的每个当前项相关。 名称 ARTXP 派生自以下事实，即自动回归树方法（一种 ART 算法）应用于多个未知的先前状态。 有关 ARTXP 算法的详细说明，请参阅 [序分析的自动回归树模型](https://go.microsoft.com/fwlink/?LinkId=45966)。  
  
 该 ARIMA 算法已添加到 SQL Server 2008 的 Microsoft 时序算法中，用于提高长期预测的准确性。 它是 Box 和 Jenkins 描述的用于计算自动回归集成变动平均值的过程的实现。 通过 ARIMA 方法，可以确定按时间顺序进行的观察中的依赖关系，并且可以将随机冲量作为模型的一部分纳入。 该 ARIMA 方法还支持倍乘季节性。 想要了解有关 ARIMA 算法的详细信息的读者最好阅读 Box 和 Jenkins 在论坛上发布的内容；本节旨在提供关于 ARIMA 算法如何在 Microsoft 时序算法中实施的特定详细信息。  
  
 默认情况下，Microsoft 时序算法通过使用 ARIMA 和 ARTXP 这两种算法并混合所得到的结果来改进预测准确性。 如果您想要仅使用特定的方法，则可以将算法参数设置为仅使用 ARTXP 或仅使用 ARIMA，或者控制对算法结果进行组合的方式。 请注意，ARTXP 算法支持交叉预测，但 ARIMA 算法不支持。 因此，只有在使用混合算法或将模型配置为仅使用 ARTXP 时，交叉预测才可用。  
  
## <a name="understanding-arima-difference-order"></a>理解 ARIMA 差分阶数  
  本节介绍理解 ARIMA 模型所需的一些术语，并且论述在 Microsoft 时序算法中的特定“差分”实现方式。 有关这些项和概念的完整解释，我们建议您参阅 Box 和 Jenkins 的著述。  
  
-   项是数学方程式中的一个组成部分。 例如，多项式方程式中的项可以包括变量和常量的组合。  
  
-    在 Microsoft 时序算法中包括的 ARIMA 公式使用“自动回归”  和“移动平均值”这两个项。  
  
-    时序模型可以是“静态的” 或“非静态的”。  “静态模型”  是还原为平均值的那些模型（尽管它们可能具有循环），而“非静态模型” 不具有平衡焦点，需要承受“充量”或外部变量引入的更大差异或变化。  
  
-    “差分”的目标是使时序稳定且变得静态。  
  
-   “差分阶数”   表示为时序取的值之间的差分的次数。  
  
 Microsoft 时序算法的工作方式是在某一数据序列中取值，然后尝试将数据适合于某一模式。 如果该数据序列已不是静态的，则该算法将应用差分阶数。 差分阶数中的每个增加都往往使该时序更为静态。  
  
 例如，如果具有时序 （z1，z2，...，zn） 并且使用一个差分阶数执行计算，您将获取一个新时序 (y1，y2，...，yn-1)，其中*彝语 = zi + 1-zi*。 在差分阶数为 2 时，该算法将生成基于已从第一个阶数方程式派生的 y 时序的另一个时序 （x1，x2，...，xn-2）。 差分的正确量依赖于数据。 单个差分阶数在显示不变趋势的模型中最常见；第二个差分阶数可指示随着时间而变化的趋势。  
  
 默认情况下，在 Microsoft 时序算法中使用的差分阶数为 -1，这意味着该算法将自动检测差分阶数的最佳值。 通常，该最佳值为 1（在需要差分时），但在某些情况下，该算法将该值增加到最大值 2。  
  
 Microsoft 时序算法通过使用自动回归值确定最佳的 ARIMA 差分阶数。 该算法检查 AR 值并且设置一个隐藏的参数 ARIMA_AR_ORDER，这表示 AR 项的阶数。 此隐藏的参数 ARIMA_AR_ORDER 的值范围是从 -1 到 8。 在为默认值 -1 时，该算法将自动选择适当的差分阶数。  
  
 只要 ARIMA_AR_ORDER 的值大于 1，该算法就将时序乘以多项式项。 如果多项式公式的一个项解析为 1 的根或接近 1，则该算法将尝试通过删除该项并将差分阶数增加 1，保持该模型的稳定性。 如果差分阶数已是最大值，则该项将删除并且差分阶数不更改。  
  
 例如，如果 AR 的值 = 2，则生成的 AR 多项式项可能如下所示：1-1.4 B +.45B ^2 = (1-.9B) (1-0.5B)。 请注意具有大约 0.9 的根的术语 (1-.9B)。 该算法从多项式公式中清除此项，但无法将差分阶数增加 1，因为该差分阶数已处于最大值 2。  
  
 务须注意的是：唯一能够 **强制** 更改差分阶数的方式就是使用不受支持的参数 ARIMA_DIFFERENCE_ORDER。 这个隐藏参数控制算法对时序执行差分的次数，可以通过键入自定义算法参数来设置该参数。 但是，我们不建议您更改此值，除非您已经做好试验的准备，并且熟悉会涉及到的计算。 还请注意，目前没有任何机制（包括隐藏参数）可供您控制触发差分阶数增加的阈值。  
  
 最后要注意的是，上述公式为简化的情况，没有季节性提示。 如果提供季节性提示，则对于每个季节性提示，单独的 AR 多项式项将添加到方程式的左侧，并且将应用相同的策略以便消除可能导致差分序列不稳定的项。  
  
## <a name="customizing-the-microsoft-time-series-algorithm"></a>自定义 Microsoft 时序算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序算法支持以下参数，这些参数会影响所生成挖掘模型的行为、性能和精确性。  
  
> [!NOTE]  
>  在所有版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中均提供 Microsoft 时序算法；但是，仅在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的特定版本中才支持某些高级功能，包括用于自定义时序分析的参数。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2012 各个版本支持的功能](https://go.microsoft.com/fwlink/?linkid=232473)。  
  
### <a name="detection-of-seasonality"></a>季节性检测  
 ARIMA 和 ARTXP 算法都支持季节性检测或周期检测。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在定型之前使用快速傅立叶变换检测季节性。 但是，您可以通过设置算法参数，影响季节性检测以及时序分析的结果。  
  
-   通过更改 AUTODETECT_SEASONALITY 的值，可以影响生成的时间段的可能数目。  
  
-   通过为 PERIODICITY_HINT 设置一个值或多个值，可以为算法提供有关数据中预期周期的信息并有可能提高检测精度。  
  
> [!NOTE]  
>  ARTXP 和 ARIMA 算法都对季节性提示非常敏感。 因此，提供错误提示可能会对结果产生不利影响。  
  
### <a name="choosing-an-algorithm-and-specifying-the-blend-of-algorithms"></a>选择算法和指定算法混合  
 默认情况下，在选择 MIXED 选项时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会将算法组合起来并向它们分配相等的权重。 不过，在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 中，可以指定特定的算法，或者可以通过设置参数来自定义结果中各算法的比例，该参数针对短期预测或长期预测为结果加权。 默认情况下，FORECAST_METHOD 参数将设置为 MIXED，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用这两个算法，并对其值加权以最大化每个算法的强度。  
  
-   若要控制算法选择，可以设置 FORECAST_METHOD 参数。  
  
-   如果要使用交叉预测，则必须使用 ARTXP 或 MIXED 选项，原因是 ARIMA 不支持交叉预测。  
  
-   如果更看重短期预测，则将 FORECAST_METHOD 设置为 ARTXP。  
  
-   如果想要改进长期预测，则将 FORECAST_METHOD 设置为 ARIMA。  
  
 在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]中，还可以自定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 混合使用 ARIMA 和 ARTXP 算法组合的方式。 可以通过设置 PREDICTION_SMOOTHING 参数控制混合的起点和变化速率：  
  
-   如果将 PREDICTION_SMOOTHING 设置为 0，则模型将仅使用 ARTXP。  
  
-   如果将 PREDICTION_SMOOTHING 设置为 1，则模型将仅使用 ARIMA。  
  
-   如果将 PREDICTION_SMOOTHING 设置为 0 和 1 之间的某个值，则模型对 ARTXP 算法所加的权重将随着预测步长增加而按指数规律减小。 同时，模型还将 ARIMA 算法的权重设置为 ARTXP 权重的 1 补数。 模型使用规范化和一个稳定常量来平滑曲线。  
  
 一般来说，如果最多预测 5 个时间段，则 ARTXP 几乎总是最佳选择。 但是，当增加要预测的时间段的个数时，ARIMA 的性能通常会更好。  
  
 下图演示当 PREDICTION_SMOOTHING 设置为默认值 0.5 时模型如何混合使用这两个算法。 ARIMA 和 ARTXP 开始时权重相等，但随着预测步骤数增加，ARIMA 的权重越来越大。  
  
 ![时序算法混合的默认曲线](../media/time-series-mixing-default.gif "时序算法混合的默认曲线")  
  
 而下图演示当 PREDICTION_SMOOTHING 设置为 0.2 时如何混合使用这两个算法。 对于步骤 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]，模型为 ARIMA 加的权重为 0.2，为 ARTXP 加的权重为 0.8。 此后，ARIMA 的权重将按指数规律增大，而 ARTXP 的权重将按指数规律减小。  
  
 ![时序模型混合的衰减曲线](../media/time-series-blending-curve.gif "时序模型混合的衰减曲线")  
  
### <a name="setting-algorithm-parameters"></a>设置算法参数  
 下表介绍可用于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序算法的参数。  
  
|参数|Description|  
|---------------|-----------------|  
|*AUTO_DETECT_PERIODICITY*|指定一个介于 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] 和 1 之间的数值，用于检测周期。 默认值为 0.6。<br /><br /> 如果将此值设置为比较接近于 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]的数，则只检测周期性强的数据的周期。<br /><br /> 如果将此值设置为比较接近于 1 的数，则往往会发现许多接近周期的模式并倾向于自动生成周期提示。<br /><br /> 注意：处理大量的周期提示可能会导致模型定型时间明显延长，不过模型会更精确。|  
|*COMPLEXITY_PENALTY*|控制决策树的增长。 默认值为 0.1。<br /><br /> 减少该值将增大拆分的几率。 增大该值将减小拆分的几率。<br /><br /> 注意：此参数仅在某些版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用。|  
|*FORECAST_METHOD*|指定要用于分析和预测的算法。 可能值为 ARTXP、ARIMA 或 MIXED。 默认值为 MIXED。|  
|*HISTORIC_MODEL_COUNT*|指定将要生成的历史模型的数量。 默认值为 1。<br /><br /> 注意：此参数仅在某些版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用。|  
|*HISTORICAL_MODEL_GAP*|指定两个连续的历史模型之间的时间间隔。 默认值为 10。 该值表示时间单位数，其中单位由模型定义。<br /><br /> 例如，如果将此值设置为 g，则将以 g、2*g、3\*g（依此类推）的时间间隔为被时间段截断的数据生成历史模型。<br /><br /> 注意：此参数仅在某些版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用。|  
|*INSTABILITY_SENSITIVITY*|控制预测方差超过特定阈值的点，在该点后 ARTXP 算法将禁止预测。 默认值为 1。<br /><br /> 注意：此参数不适用于仅使用 ARIMA 的模型。<br /><br /> 默认值 1 提供与 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]相同的行为。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 监视每个预测的规范化标准偏差。 对于任何预测，只要该值超过阈值，时序算法就会返回 NULL 并停止预测过程。<br /><br /> 值 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] 将停止不稳定的检测。 这意味着无论方差为多少，都可以创建无限个预测。<br /><br /> 注意：此参数只能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 中进行修改。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard 中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 仅使用默认值 1。|  
|*MAXIMUM_SERIES_VALUE*|指定用于预测的最大值。 此参数与 MINIMUM_SERIES_VALUE 一起用于将预测约束到某一预期范围。 例如，您可以指定任何一天的预测销售数量决不应超过库存产品数量。<br /><br /> 注意：此参数仅在某些版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用。|  
|*MINIMUM_SERIES_VALUE*|指定可以预测的最小值。 此参数与 MAXIMUM_SERIES_VALUE 一起用于将预测约束到某一预期范围。 例如，可以指定预测的销售额决不应为负数。<br /><br /> 注意：此参数仅在某些版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用。|  
|*MINIMUM_SUPPORT*|指定在每个时序树中生成一个拆分所需的最小时间段数。 默认值为 10。|  
|*MISSING_VALUE_SUBSTITUTION*|指定如何填补历史数据中的空白。 默认情况下，不允许数据中存在空白。 如果数据中包含多个序列，则序列也不能有参差不齐的边缘。 也就是说，所有序列都应具有相同的起点和终点。 对时序模型执行 `PREDICTION JOIN` 时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还使用此参数的值来填补新数据中的空白。 下表将列出此参数的可能值：<br /><br /> None:默认值。 用沿定型模型曲线绘制的值来替换缺失值。<br /><br /> 上一：重复前一时间段中的值。<br /><br /> 平均值：使用定型时所用的时间段的变动平均值。<br /><br /> 数值常量：使用指定的数字来替换所有缺失值。|  
|*PERIODICITY_HINT*|提供算法的有关数据周期的提示。 例如，如果销售额按年度变化，且序列中的度量单位是月，则周期为 12。 此参数采用 {n [, n]} 格式，其中 n 为任意正数。<br /><br /> 方括号 [] 中的 n 是可选项，并且可以按需多次重复。 例如，若要为按月提供的数据提供多个周期提示，则可以输入 {12, 3, 1} 来检测年度、季度和月的模式。 但是，周期对模型质量有重大影响。 如果给出的提示与实际周期不同，则会对结果造成不良影响。<br /><br /> 默认值为 {1}。<br /><br /> 注意：需要使用大括号。 另外，此参数具有字符串数据类型。 因此，如果在数据挖掘扩展插件 (DMX) 语句中键入此参数，则必须用引号将数字和大括号括起来。|  
|*PREDICTION_SMOOTHING*|指定应如何混合模型以优化预测。 此参数仅在某些版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用。 可以键入 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] 和 1 之间的任何值，也可以使用以下值之一：<br /><br /> [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]设置用户帐户 ：指定预测仅使用 ARTXP。 针对较少的预测来优化预测。<br /><br /> 0.5:（默认值）指定预测时两个算法都应使用并混合结果。<br /><br /> 1：指定预测仅使用 ARIMA。 针对多个预测来优化预测。<br /><br /> <br /><br /> 注意：使用*FORECAST_METHOD*参数来控制定型。|  
  
### <a name="modeling-flags"></a>建模标志  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序算法支持下列建模标志。 创建挖掘结构或挖掘模型时，定义建模标志以指定分析期间如何处理每列中的值。 有关详细信息，请参阅[建模标志（数据挖掘）](modeling-flags-data-mining.md)。  
  
|建模标志|Description|  
|-------------------|-----------------|  
|NOT NULL|指示该列不能包含 Null。 如果 Analysis Services 在模型定型过程中遇到 Null 值，将会导致错误。<br /><br /> 适用于挖掘结构列。|  
|MODEL_EXISTENCE_ONLY|表示该列将被视为具有两个可能状态:Missing 和 Existing。 Null 表示缺失值。<br /><br /> 适用于挖掘模型列。|  
  
## <a name="requirements"></a>要求  
 时序模型中必须包含一个含有唯一值的 Key Time 列、输入列以及至少一个可预测列。  
  
### <a name="input-and-predictable-columns"></a>输入列和可预测列  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序算法支持特定的输入列内容类型、可预测列内容类型和建模标志，如下表所列。  
  
|“列”|内容类型|  
|------------|-------------------|  
|输入属性|Continuous、Key、Key Time 和 Table|  
|可预测属性|Continuous 和 Table|  
  
> [!NOTE]  
>  支持 Cyclical 和 Ordered 内容类型，但算法会将它们视为离散值，不会进行特殊处理。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 时序算法](microsoft-time-series-algorithm.md)   
 [时序模型查询示例](time-series-model-query-examples.md)   
 [时序模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
