---
title: 功能选择（数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], feature selections
- attributes [data mining]
- feature selection algorithms [Analysis Services]
- data mining [Analysis Services], feature selections
- neural network algorithms [Analysis Services]
- naive bayes algorithms [Analysis Services]
- decision tree algorithms [Analysis Services]
- datasets [Analysis Services]
- clustering algorithms [Analysis Services]
- coding [Data Mining]
ms.assetid: b044e785-4875-45ab-8ae4-cd3b4e3033bb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a1d79bb3810a56e8a1769845131312eab306f223
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084419"
---
# <a name="feature-selection-data-mining"></a>功能选择（数据挖掘）
  *功能选择*是数据挖掘中常用的一种术语，用于描述可用于将输入减少到可管理的大小以进行处理和分析的工具和技术。 功能选择不仅意味着*基数降低*，还意味着对在生成模型时可以考虑的属性数量施加任意或预定义的截止时间，同时也意味着选择属性，这意味着分析师或建模工具会根据分析的有用性主动选择或放弃属性。  
  
 能够应用功能选择对于有效分析至关重要，因为数据集包含的信息通常多于生成模型所需的信息。 例如，一个数据集可能包含 500 个用来描述客户特征的列，但是，如果其中某些列的数据非常稀疏，则您从将这些数据添加到模型中所得到的利益可能会非常少。 如果在生成模型时保留不需要的列，则定型期间需要更多的 CPU 和内存，并且已完成的模型需要更多的存储空间。  
  
 即使资源不存在任何问题，由于不需要的列可能因为下列原因而降低发现的模式的质量，因此通常需要删除这些列：  
  
-   某些列存在干扰或冗余。 此干扰会使从数据中发现有意义的模式更困难；  
  
-   若要发现质量模式，大多数数据挖掘算法需要高维数据集上的较大定型数据集。 但是某些数据挖掘应用程序中的定型数据非常少。  
  
 在数据源的这 500 列中，如果只有 50 列具有在生成模型时有用的信息，则您可以只将这些列保持在模型之外，或者可以使用功能选择技术自动发现最佳功能并且排除在统计上无用的值。 功能选择有助于解决两个问题：无价值的数据过多或有价值的数据过少。  
  
## <a name="feature-selection-in-analysis-services-data-mining"></a>Analysis Services 数据挖掘中的功能选择  
 通常，功能选择在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中自动执行，并且每个算法都具有用于智能地应用功能选择的一组默认技术。 功能选择始终在对模型进行定型之前执行，以自动选择数据集中最有可能在该模型中使用的属性。 但是，您也可以手动设置参数以便影响功能选择行为。  
  
 通常，功能选择的工作方式是为每个属性计算一个分数，然后仅选择具有最高分数的属性。 您还可以调整最高分数的阈值。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供多种方法来计算这些分数，适用于任何模型的准确方法取决于以下因素：  
  
-   在模型中使用的算法  
  
-   属性的数据类型  
  
-   可对模型设置的任何参数  
  
 功能选择应用于输入、可预测属性或列中的状态。 在用于功能选择的分数完整时，只有算法选择的属性和状态才会包含在模型生成过程中并可用于预测。 即使您选择的可预测属性未满足用于功能选择的阈值，这些属性仍可用于预测，但这些预测将只是基于模型中存在的全局统计信息进行的。  
  
> [!NOTE]  
>  功能选择仅影响模型中使用的列，而对挖掘结构的存储没有任何影响。 留在挖掘模型之外的列仍在结构中可用，并将缓存挖掘结构列中的数据。  
  
### <a name="definition-of-feature-selection-methods"></a>功能选择方法的定义  
 实现功能选择的方法很多，具体取决于使用的数据类型以及为分析选择的算法。 SQL Server Analysis Services 提供了用于对属性进行计分的若干现成的常用方法。 在任何算法或数据集中应用的方法取决于数据类型和列的用法。  
  
 “兴趣性 ** ”分数用于对包含非二进制连续数值数据的列中的属性进行排列和排序。  
  
 ** “Shannon 平均信息量”和两个“Bayesian” ** 分数可用于包含离散和离散化数据的列。 但是，如果模型包含任何连续列，则兴趣性分数将用于评估所有的输入列，以确保一致性。  
  
 下面的部分对功能选择的每种方法分别进行了介绍。  
  
#### <a name="interestingness-score"></a>兴趣性分数  
 如果某个功能可以提供一些有用的信息，则该功能很令人感兴趣。 由于具体方案的定义很有用，具体取决于方案，数据挖掘行业开发了多种方法来度量*兴趣性*。 例如，*新奇*可能会在离群值检测中感兴趣，但在密切相关的项目或*对比权重*之间进行区分的能力可能更适合分类。  
  
 SQL Server Analysis Services 中使用的兴趣性的度量值是*基于平均信息量*的，这意味着具有随机分布的属性具有较高的平均信息量和较低的信息增益;因此，此类属性的意义不大。 任何特定属性的平均信息量都将与所有其他属性的平均信息量进行比较，如下所示：  
  
 Interestingness(Attribute) = - (m - Entropy(Attribute)) * (m - Entropy(Attribute))  
  
 中央平均信息量（即 m）表示整个功能集的平均信息量。 通过用中央平均信息量减去目标属性的平均信息量，可以评估该属性提供了多少信息。  
  
 每当列包含非二进制连续数值数据时，就会默认使用此分数。  
  
#### <a name="shannons-entropy"></a>Shannon 平均信息量  
 Shannon 平均信息量针对特定的结果度量随机变量的不确定性。 例如，抛硬币的平均信息量可以表示为其正面朝上概率的函数。  
  
 Analysis Services 使用以下公式来计算 Shannon 平均信息量：  
  
 H(X) = -  P(xi) log(P(xi))  
  
 此计分方法适用于离散和离散化的属性。  
  
#### <a name="bayesian-with-k2-prior"></a>Bayesian with K2 Prior  
 Analysis Services 提供了两种基于 Bayesian 网络的功能选择分数。 Bayesian 网络是状态的“定向 ** ”或“非循环 ** ”曲线图，也是状态间的转换，这意味着某些状态始终早于当前的状态，某些状态是较晚的，曲线图不会重复或循环。 根据定义，Bayesian 网络允许使用先前的知识。 但是，对于算法设计、性能和精确度而言，关于在以后状态的概率计算中要使用以前的哪一个状态的问题是很重要的。  
  
 从 Bayesian 网络中了解的 K2 算法是由 Cooper 和 Herskovits 开发的，经常在数据挖掘中使用。 该算法是可伸缩的，并可以分析多个变量，但需要对用作输入的变量进行排序。 有关详细信息，请参阅由 Chickering、Geiger 和 Heckerman 编写的 [了解 Bayesian 网络](https://go.microsoft.com/fwlink/?LinkId=105885) 。  
  
 此计分方法适用于离散和离散化的属性。  
  
#### <a name="bayesian-dirichlet-equivalent-with-uniform-prior"></a>Bayesian Dirichlet Equivalent with Uniform Prior  
 Bayesian Dirichlet Equivalent (BDE) 分数还使用 Bayesian 分析来评估给定数据集的网络。 BDE 计分方法是由 Heckerman 开发的，并基于 Cooper 和 Herskovits 开发的 BD 指标。 Dirichlet 分布是描述网络中每个变量的条件概率的多项分布，其中很多属性对学习很有用。  
  
 Bayesian Dirichlet Equivalent with Uniform Prior (BDEU) 方法假定一个 Dirichlet 分布的特殊事例，在这个事例中使用一个数学常量创建一个以前状态的固定或均匀分布。 BDE 分数还假定可能性均等，这意味着数据不应当用来区分相等的结构。 也就是说，如果 If A Then B 的分数与 If B Then A 的分数相同，则无法基于数据区分这两种结构，也无法推断因果关系。  
  
 有关 Bayesian 网络和这些计分方法实现的详细信息，请参阅 [Learning Bayesian Networks](https://go.microsoft.com/fwlink/?LinkId=105885)（了解 Bayesian 网络）。  
  
### <a name="feature-selection-methods-used-by-analysis-services-algorithms"></a>Analysis Services 算法使用的功能选择方法  
 下表列出了支持功能选择的算法、该算法所使用的功能选择方法以及设置用于控制功能选择行为的参数：  
  
|算法|分析方法|说明|  
|---------------|------------------------|--------------|  
|Naive Bayes|Shannon 平均信息量<br /><br /> Bayesian with K2 Prior<br /><br /> 使用统一先验的 Bayesian Dirichlet（默认）|Microsoft Naïve Bayes 算法仅接受离散或离散化的属性，因此它不能使用兴趣性分数。<br /><br /> 有关此算法的详细信息，请参阅 [Microsoft Naive Bayes Algorithm Technical Reference](microsoft-naive-bayes-algorithm-technical-reference.md)。|  
|决策树|兴趣性分数<br /><br /> Shannon 平均信息量<br /><br /> Bayesian with K2 Prior<br /><br /> 使用统一先验的 Bayesian Dirichlet（默认）|如果任何列包含非二进制连续值，则兴趣性分数将用于所有列，以确保一致性。 否则，将使用默认的功能选择方法或者您在创建模型时指定的方法。<br /><br /> 有关此算法的详细信息，请参阅 [Microsoft Decision Trees Algorithm Technical Reference](microsoft-decision-trees-algorithm-technical-reference.md)。|  
|神经网络|兴趣性分数<br /><br /> Shannon 平均信息量<br /><br /> Bayesian with K2 Prior<br /><br /> 使用统一先验的 Bayesian Dirichlet（默认）|只要数据包含连续列，Microsoft 神经网络算法就可同时使用基于平均信息量的方法和 Bayesian 方法。<br /><br /> 有关此算法的详细信息，请参阅 [Microsoft Neural Network Algorithm Technical Reference](microsoft-neural-network-algorithm-technical-reference.md)。|  
|逻辑回归|兴趣性分数<br /><br /> Shannon 平均信息量<br /><br /> Bayesian with K2 Prior<br /><br /> 使用统一先验的 Bayesian Dirichlet（默认）|虽然 Microsoft 逻辑回归算法基于 Microsoft 神经网络算法，但您不能自定义逻辑回归模型以控制功能选择行为；因此，功能选择始终默认为最适合该属性的方法。<br /><br /> 如果所有属性均为离散或离散化属性，则默认值为 BDEU。<br /><br /> 有关此算法的详细信息，请参阅 [Microsoft Logistic Regression Algorithm Technical Reference](microsoft-logistic-regression-algorithm-technical-reference.md)。|  
|聚类分析|兴趣性分数|Microsoft 聚类分析算法可以使用离散或离散化数据。 但是，每个属性的分数仍将作为距离进行计算并且表示为连续数字，因此必须使用兴趣性分数。<br /><br /> 有关此算法的详细信息，请参阅 [Microsoft Clustering Algorithm Technical Reference](microsoft-clustering-algorithm-technical-reference.md)。|  
|线性回归|兴趣性分数|因为仅支持连续列，Microsoft 线性回归性算法只能使用兴趣性分数。<br /><br /> 有关此算法的详细信息，请参阅 [Microsoft Linear Regression Algorithm Technical Reference](microsoft-linear-regression-algorithm-technical-reference.md)。|  
|关联规则<br /><br /> 顺序分析和聚类分析|未使用|不使用这些算法调用功能选择。<br /><br /> 但在必要时，可以通过设置参数 MINIMUM_SUPPORT 和 MINIMUM_PROBABILIITY 的值来控制算法的行为和减小输入数据的大小。<br /><br /> 有关详细信息，请参阅 [Microsoft Association Algorithm Technical Reference](microsoft-association-algorithm-technical-reference.md) 和 [Microsoft Sequence Clustering Algorithm Technical Reference](microsoft-sequence-clustering-algorithm-technical-reference.md)。|  
|时序|未使用|功能选择不适用于时序模型。<br /><br /> 有关此算法的详细信息，请参阅 [Microsoft Time Series Algorithm Technical Reference](microsoft-time-series-algorithm-technical-reference.md)。|  
  
## <a name="feature-selection-parameters"></a>功能选择参数  
 在支持功能选择的算法中，可以使用下列参数来控制何时打开功能选择。 对于所允许的输入数目，每个算法都有一个默认值，但您可以覆盖此默认值并指定属性的数目。 本节列出了为管理功能选择而提供的参数。  
  
#### <a name="maximum_input_attributes"></a>MAXIMUM_INPUT_ATTRIBUTES  
 如果某个模型包含的列多于 *MAXIMUM_INPUT_ATTRIBUTES* 参数中指定的数目，算法将忽略它计算后认为无用的任何列。  
  
#### <a name="maximum_output_attributes"></a>MAXIMUM_OUTPUT_ATTRIBUTES  
 同样，如果某个模型包含的可预测列多于 *MAXIMUM_OUTPUT_ATTRIBUTES* 参数中指定的数目，算法将忽略它计算后认为无用的任何列。  
  
#### <a name="maximum_states"></a>MAXIMUM_STATES  
 如果某个模型包含的事例多于 *MAXIMUM_STATES* 参数中指定的数目，则最不常见的状态将被分组在一起且被视为不存在。 如果这些参数中的任何一个被设置为 0，则功能选择将被关闭，这会影响处理时间和性能。  
  
 除了上述用于功能选择的方法之外，您还可以通过对模型设置“建模标志” ** 或者对结构设置“分布标志” ** ，提高算法标识或改进有意义属性的能力。 有关这些概念的详细信息，请参阅[建模标志（数据挖掘）](modeling-flags-data-mining.md)和[列分布（数据挖掘）](column-distributions-data-mining.md)。  
  
## <a name="see-also"></a>另请参阅  
 [自定义挖掘模型和结构](customize-mining-models-and-structure.md)  
  
  
