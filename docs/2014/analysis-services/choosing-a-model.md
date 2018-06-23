---
title: 选择模型 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data mining algorithms
- mining models
- mining structures
- data mining models
- data mining structures
ms.assetid: 444bbf9c-cec8-460e-881d-38784fb146fa
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 60cba88e3674e72fc824edf450bdbd87ae4e4aea
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138557"
---
# <a name="choosing-a-model"></a>选择模型
  **挖掘算法：** 数据挖掘*算法*是从数据创建模式的机制。 此算法可定义如何对数据进行计数、如何推断出关系以及如何存储模式。 算法的选择部分取决于要分析的数据的类型。 例如，一些算法仅适用于连续数字，而其他算法则适用于有限数目的非重复值。  
  
 **挖掘模型：** 算法的数据分析的结果保存在*挖掘模型*。 挖掘模型是规则、统计信息和模式的集合。 *内容*挖掘模型取决于你用来处理数据，但可能包括以下算法：  
  
-   说明在事务中如何将产品分组到一起的 If-then 规则。  
  
-   决策树，它跟踪导致某个结果的路径并列出每个路径的出现概率。  
  
-   具有等式的数学模型，可用于整个模型或用于模型的某些段。  
  
-   相似的项目的集合 (称为*群集*或*段*) 定义由它们共享的特征和相似性得分。  
  
-   *节点*在网络中，通过连接*边缘*。 节点表示项或项组。 根据节点间的关系强度赋予边缘分数。  
  
 **使用模型：** 后创建一个模型，可以使用提供的查看器浏览它，或者可以创建针对模型的查询。 查询可用于：  
  
-   预测将来值。  
  
-   生成一组相关的产品或推荐的产品。  
  
-   返回模型中的规则、模式或公式。  
  
-   从模型中获取元数据。  
  
-   为所有或某些预测提供概率和支持得分。  
  
## <a name="types-of-machine-learning-algorithms"></a>计算机学习算法的类型  
 因为不同类型的算法使用数据的方法不同，所以，在创建模型时，必须选择适合于您的目标和要分析的数据的算法。  
  
 Excel 数据挖掘外接程序包括以下多种算法类型：  
  
-   *分类算法*。  
  
     基于数据集中的其他属性预测一个或多个离散变量。  
  
-   *回归算法*  
  
     基于数据集中的其他属性预测一个或多个连续变量，如利润或亏损。  
  
-   *分段算法*  
  
     将数据划分为组或分类，这些组或分类的项具有相似的属性。  
  
-   *关联算法*  
  
     查找数据集中不同属性之间的相关性。 此类算法通常用于创建关联规则。 关联规则可用于市场篮分析。  
  
-   *顺序分析算法*  
  
     汇总数据中的常见顺序或事件，如用户在浏览网站时所遵循的路径。  
  
 SQL Server Office 数据挖掘外接程序所使用的算法基于 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供的算法。 如果，也可以使用符合 OLE DB 数据挖掘规范的第三方算法的实例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]你连接到已配置为允许第三方算法。  
  
## <a name="requirements"></a>要求  
 每种算法可以使用的数据类型不同。  
  
-   线性回归模型只能对数值建模。 您的输入变量和目标结果必须为连续数字类型。 如果必须混合离散变量和连续变量，请使用决策树或估计模型。  
  
-   Naïve Bayes 模型要求将所有数字装箱。 如果使用基于此算法的某个向导，则自动为您执行装箱。  
  
-   决策树模型可以同时包含离散变量和连续变量。 但是，数字将根据树中的拆分需要自动装箱。  
  
-   神经网络和逻辑回归模型自动将使用的数字装箱为结果或输入变量。 如果要根据其他一些条件将数字分组，应在建模前使用重新标记工具来创建分组。 例如，你可能需要组中的值**年龄**deciles （10 20、 21-30 等等），由一列，而不是具有统计学意义的分组 （一个示例可能是 35.6 41.8 年） 该模型发现的。  
  
-   关联模型要求按交易将数据分组，每个指代几个商品或行。 如果你使用[关联向导&#40;for Excel 数据挖掘客户端&#41;](associate-wizard-data-mining-client-for-excel.md)向导或[购物篮分析&#40;for Excel 表 AnalysisTools&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md)工具，数据应缩小中所示放置**关联**的示例工作簿的选项卡。  
  
     如果你想要使用的外部数据源中的嵌套的表，则必须使用[高级建模&#40;数据挖掘外接程序 Excel&#41; ](advanced-modeling-data-mining-add-ins-for-excel.md)建模选项可创建挖掘结构和挖掘模型保存在服务器上。 Excel 不支持嵌套的表。  
  
## <a name="feature-selection"></a>功能选择  
 具体取决于数据集，该算法可能会应用*功能选择*、 除去列并没有用处，并确定哪些列的数据是相对于结果具有统计学意义。  
  
 每种算法都使用略微不同的功能选择方法（例如平均信息量或不同信息分数）来确定哪些趋势比较重要，哪些差异可以忽略。  
  
 在 Excel 数据挖掘外接程序中，使用对每个算法合适的得分方法自动应用功能选择。 如果你想要影响的功能选择结果集，使用在向导**数据挖掘**功能区，然后单击**高级**设置使用的参数**算法参数**对话框。  
  
 功能选择的列表所使用的每个算法方法请参阅主题上[功能选择&#40;数据挖掘&#41;](data-mining/feature-selection-data-mining.md) SQL Server 联机丛书中。  
  
## <a name="list-of-supported-algorithms"></a>支持的算法列表  
 默认情况下提供以下算法：  
  
|算法名称|Description|适用范围|  
|--------------------|-----------------|-------------|  
|Microsoft 关联规则|生成一些规则，说明哪些项有可能同时出现在一个交易中。|[关联向导&#40;for Excel 数据挖掘客户端&#41;](associate-wizard-data-mining-client-for-excel.md)<br /><br /> [购物篮分析&#40;的 Excel 表 AnalysisTools&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)|  
|Microsoft 聚类分析|标识数据集中可能无法通过随意观察在逻辑上得出的关系。 该算法使用迭代技术将记录分组为包含类似特征的分类。|[检测类别&#40;的 Excel 表分析工具&#41;](detect-categories-table-analysis-tools-for-excel.md)<br /><br /> [群集向导&#40;数据挖掘的 Excel 外接程序&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)|  
|Microsoft 决策树|根据数据集中各列之间的关系进行预测，然后采用树状分支序列形式基于特定值对这些关系建模。<br /><br /> 同时支持对离散属性和连续属性的预测。|[分类向导&#40;数据挖掘的 Excel 外接程序&#41;](classify-wizard-data-mining-add-ins-for-excel.md)<br /><br /> [估计向导&#40;数据挖掘的 Excel 外接程序&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)|  
|Microsoft 线性回归|如果目标变量和要检查的变量之间存在线性依赖关系，则将找出目标与其输入之间最有效的关系。<br /><br /> 支持对连续属性的预测。|此算法在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中提供。 在 Office 数据挖掘外接程序中，可以通过创建结构然后手动添加模型的方式来创建使用此算法的模型。<br /><br /> 有关详细信息，请参阅[高级建模&#40;for Excel 的数据挖掘外接&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)。|  
|Microsoft 逻辑回归|分析导致结果的因素，其中结果被限定为两个值，通常表示某事件是发生还是不发生。<br /><br /> 同时支持对离散属性和连续属性的预测。|[从示例填充&#40;的 Excel 表分析工具&#41;](fill-from-example-table-analysis-tools-for-excel.md)<br /><br /> [目标查找方案&#40;的 Excel 表分析工具&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)<br /><br /> [假设分析方案&#40;的 Excel 表分析工具&#41;](what-if-scenario-table-analysis-tools-for-excel.md)<br /><br /> [预测计算器&#40;的 Excel 表分析工具&#41;](prediction-calculator-table-analysis-tools-for-excel.md)|  
|Microsoft Naïve Bayes|算出所有输入列与可预测列之间的关系的概率。 该算法能够快速生成挖掘模型，以发现输入列和可预测列之间的关系。<br /><br /> 仅支持离散属性或离散化的属性。<br /><br /> 将所有输入属性都视为独立属性。|[分析关键影响因素&#40;的 Excel 表分析工具&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)|  
|Microsoft 神经网络|分析复杂的输入数据或业务问题，适合有大量定型数据但使用其他算法很难找出规则的情况。<br /><br /> 可以预测多种属性。<br /><br /> 可用于对离散属性和连续属性的回归进行分类。|此算法在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中提供。 在 Office 数据挖掘外接程序中，可以通过创建结构然后手动添加模型的方式来创建使用此算法的模型。<br /><br /> 有关详细信息，请参阅[高级建模&#40;for Excel 的数据挖掘外接&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)。|  
|Microsoft 顺序分析和聚类分析|找出序列中排序方式类似的事件所组成的分类。<br /><br /> 将顺序分析和聚类分析组合在一起。|此算法仅在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中提供。 但是，在 Office 数据挖掘外接程序中，您可以通过创建结构然后手动添加模型的方式来创建使用此算法的模型。<br /><br /> 有关详细信息，请参阅[高级建模&#40;for Excel 的数据挖掘外接&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)。|  
|Microsoft 时序|使用线性决策树分析与时间相关的数据。<br /><br /> 模式可用于对时序中的未来值进行预测。|[预测&#40;的 Excel 表分析工具&#41;](forecast-table-analysis-tools-for-excel.md)<br /><br /> [预测向导&#40;数据挖掘的 Excel 外接程序&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)|  
  
## <a name="see-also"></a>请参阅  
 [Office 数据挖掘外接程序中包含的功能](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  