---
title: Microsoft 神经网络算法技术参考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- HIDDEN_NODE_RATIO parameter
- MAXIMUM_INPUT_ATTRIBUTES parameter
- HOLDOUT_PERCENTAGE parameter
- neural network algorithms [Analysis Services]
- output layer [Data Mining]
- neural networks
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- MAXIMUM_STATES parameter
- SAMPLE_SIZE parameter
- hidden layer
- hidden neurons
- input layer [Data Mining]
- activation function [Data Mining]
- Back-Propagated Delta Rule network
- neural network model [Analysis Services]
- coding [Data Mining]
- HOLDOUT_SEED parameter
ms.assetid: b8fac409-e3c0-4216-b032-364f8ea51095
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 118c20c16890edb50bdc19686da40c77b362c29d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48217647"
---
# <a name="microsoft-neural-network-algorithm-technical-reference"></a>Microsoft 神经网络算法技术参考
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络使用由最多三层神经元（即感知器）组成的“多层感知器”网络（也称为“反向传播 Delta 法则”网络）。 这些层分别是输入层、可选隐藏层和输出层。  
  
 有关多层感知器神经网络的详细探讨不属于本文档的讨论范围。 本主题介绍该算法的基本实现，包括用于规范化输入值与输出值的方法以及用于缩减属性基数的功能选择方法。 本主题介绍可用于自定义该算法行为的参数和其他设置，并提供与查询该模型有关的其他信息的链接。  
  
## <a name="implementation-of-the-microsoft-neural-network-algorithm"></a>Microsoft 神经网络算法的实现  
 在多层感知器神经网络中，每个神经元可接收一个或多个输入，并产生一个或多个相同的输出。 每个输出都是对神经元的输入之和的简单非线性函数。 输入将从输入层中的节点传递到隐藏层中的节点，然后再从隐藏层传递到输出层；同一层中的神经元之间没有连接。 如果像逻辑回归模型那样没有隐藏层，则输入将会直接从输入层中的节点传递到输出层中的节点。  
  
 在使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法创建的神经网络中，存在三种类型的神经元：  
  
-   `Input neurons`  
  
 输入神经元提供数据挖掘模型的输入属性值。 对于离散的输入属性，输入神经元通常代表输入属性的单个状态。 如果定型数据包含输入属性的 Null 值，则缺失的值也包括在内。 具有两个以上状态的离散输入属性会为每个状态生成一个输入神经元，如果定型数据中存在 Null 值，还会为缺失的状态生成一个输入神经元。 一个连续的输入属性将生成两个输入神经元：一个用于缺失的状态，一个用于连续属性自身的值。 输入神经元可向一个或多个隐藏神经元提供输入。  
  
-   `Hidden neurons`  
  
 隐藏神经元接收来自输入神经元的输入，并向输出神经元提供输出。  
  
-   `Output neurons`  
  
 输出神经元代表数据挖掘模型的可预测属性值。 对于离散输入属性，输出神经元通常代表可预测属性的单个预测状态，其中包括缺失的值。 例如，一个二进制可预测属性可生成一个输出节点，该节点说明缺失的或现有的状态，以指示该属性是否存在值。 一个用作可预测属性的布尔列可生成三个输出神经元：一个用于 True 值，一个用于 False 值，一个用于缺失的或现有的状态。 具有两种以上状态的离散可预测属性可为每个状态生成一个输出神经元，并为缺失的或现有的状态生成一个输出神经元。 一个连续的可预测列将生成两个输出神经元：一个用于缺失的或现有的状态，一个用于连续列自身的值。 如果检查可预测列集时生成的输出神经元多于 500 个，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将在挖掘模型中生成一个新网络，用于代表超出部分的输出神经元。  
  
 根据其所在网络层的不同，神经元接收来自其他神经元或来自其他数据的输入。 输入神经元接收来自原始数据的输入。 隐藏神经元和输出神经元接收来自神经网络中其他神经元的输出的输入。 输入在神经元之间建立了关系，而这些关系可用作分析特定事例集时的路径。  
  
 每个输入都分配有一个称为“权重” 的值，此值用于说明该特定输入对于隐藏神经元或输出神经元的相关性或重要性。 分配给一个输入的权重越大，则该输入值的相关性或重要性越高。 权重可以是负值，表示输入可能抑制而不是激活特定神经元。 每个输入的值都会与其权重相乘，以强调输入对特定神经元的重要性。 对于负权重，输入值与权重相乘的结果是降低重要性。  
  
 每个神经元都分配有一个称为激活函数的简单非线性函数，用于说明特定神经元对于神经网络层的相关性或重要性。 隐藏神经元使用双曲正切函数 (tanh) 作为其激活函数，而输出神经元使用 sigmoid 函数作为其激活函数。 这两个函数都是非线性连续函数，允许神经网络在输入神经元和输出神经元之间建立非线性关系模型。  
  
### <a name="training-neural-networks"></a>定型神经网络  
 定型使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法的数据挖掘模型时，会涉及到若干个步骤。 这些步骤与为算法参数指定的值紧密相关。  
  
 算法首先会进行评估并从数据源提取定型数据。 定型数据的百分比（称为“维持数据” ）会被保留，用于评估该网络的准确性。 在整个定型过程中，在每次迭代定型数据后，都会立即对网络进行评估。 准确性不再提高时，定型过程便会停止。  
  
 SAMPLE_SIZE 和 HOLDOUT_PERCENTAGE 参数的值用于确定定型数据中作为样本的事例数以及保留供维持数据使用的事例数。 HOLDOUT_SEED 参数的值用于随机确定保留供维持数据使用的各个事例。  
  
> [!NOTE]  
>  这些算法参数与应用于挖掘结构以定义测试数据集的属性 HOLDOUT_SIZE 和 HOLDOUT_SEED 不同。  
  
 接下来，该算法将确定挖掘模型支持的网络的数目以及复杂性。 如果挖掘模型包含一个或多个仅用于预测的属性，算法将创建一个代表所有这些属性的单一网络。 如果挖掘模型包含一个或多个同时用于输入和预测的属性，则该算法提供程序将为其中的每个属性构建一个网络。  
  
 对于具有离散值的输入属性和可预测属性，每个输入或输出神经元各自表示单个状态。 对于具有连续值的输入属性和可预测属性，每个输入或输出神经元分别表示该属性值的范围和分布。 每种情况下支持的最大状态数取决于 MAXIMUM_STATES 算法参数的值。 如果某一特定属性的状态数超过 MAXIMUM_STATES 算法参数的值，则会选出该属性最常用或相关性最高的那些状态，数目是所允许的最大状态数，剩下的状态作为缺失的值分为一组，用于分析。  
  
 然后，该算法使用 HIDDEN_NODE_RATIO 参数的值来确定要为隐藏层创建的神经元的初始数目。 可以将 HIDDEN_NODE_RATIO 设置为 0，以避免在该算法为挖掘模型生成的网络中创建隐藏层，以便将神经网络作为逻辑回归处理。  
  
 算法提供程序通过接受之前保留的定型数据集并将维持数据中的每个事例的实际已知值与网络的预测进行比较，即通过一个称为“批学习 ”的进程来同时迭代计算整个网络的所有输入的权重。 该算法处理了整个定型数据集后，将检查每个神经元的预测值和实际值。 该算法将计算错误程度（如果有错误），并调整与神经元输入关联的权重，并通过一个称为“回传” 的过程从输出神经元返回到输入神经元。 然后，该算法对整个定型数据集重复该过程。 该算法支持多个权重和输出神经元，因此这个共轭梯度算法用于引导定型过程来分配和计算输入权重。 有关共轭梯度算法的探讨不属于本文档的讨论范围。  
  
### <a name="feature-selection"></a>功能选择  
 如果输入属性数大于参数 MAXIMUM_INPUT_ATTRIBUTES 的值，或可预测属性数大于参数 MAXIMUM_OUTPUT_ATTRIBUTES 的值，则会使用功能选择算法来降低挖掘模型中包含的网络的复杂性。 功能选择可以将输入属性或可预测属性的数目减少到与该模型在统计上最相关的数目。  
  
 所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据挖掘算法都会自动使用功能选择来改善分析效果以及减轻处理工作量。 神经网络模型中用于功能选择的方法取决于属性的数据类型。 下表列出了用于神经网络模型的功能选择方法，以及用于逻辑回归算法（基于神经网络算法）的功能选择方法，以供参考。  
  
|算法|分析方法|注释|  
|---------------|------------------------|--------------|  
|神经网络|兴趣性分数<br /><br /> Shannon 平均信息量<br /><br /> Bayesian with K2 Prior<br /><br /> 使用统一先验的 Bayesian Dirichlet（默认）|只要数据包含连续列，神经网络算法就可同时使用基于平均信息量的方法和 Bayesian 计分方法。<br /><br /> 默认值。|  
|逻辑回归|兴趣性分数<br /><br /> Shannon 平均信息量<br /><br /> Bayesian with K2 Prior<br /><br /> 使用统一先验的 Bayesian Dirichlet（默认）|因为无法将参数传递给此算法来控制功能选择行为，所以将使用默认值。 因此，如果所有属性均为离散或离散化属性，则默认值为 BDEU。|  
  
 控制神经网络模型的功能选择的算法参数为 MAXIMUM_INPUT_ATTRIBUTES、MAXIMUM_OUTPUT_ATTRIBUTES 和 MAXIMUM_STATES。 您也可以通过设置 HIDDEN_NODE_RATIO 参数来控制隐藏层的数目。  
  
### <a name="scoring-methods"></a>计分方法  
 “计分” 是规范化的一种，在为神经网络模型定型的上下文中，计分表示将值（如离散文本标签）转换为可与其他输入类型进行比较且可在网络中计算权重的值。 例如，如果一个输入属性为 Gender，其可能的值为 Male 和 Female，另一个输入属性为 Income，其值范围可变，这两个属性的值不可直接比较，因此，必须编码到共同的范围，才能计算权重。 计分就是将这类输入规范化为数字值的过程：尤其是规范化为概率范围。 用于规范化的函数还有助于使输入值在统一尺度分布得更加均匀，从而避免极值扭曲分析结果。  
  
 神经网络的输出也会进行编码。 如果输出是单一目标（即预测），或者是仅用于预测而不用于输入的多个目标，模型将创建单一网络，似乎没有必要规范化输出值。 但是，如果有多个属性用于输入和预测，则模型必须创建多个网络；因此，所有值都必须规范化，输出也必须在退出网络时进行编码。  
  
 输入的编码基于对定型事例中的所有离散值进行求和以及对这些值乘以其权值。 这称为“加权和” ，它会传递给隐藏层的激活函数。 编码使用 z-score，如下所示：  
  
 **离散值**  
  
 Μ = p – 状态的先验概率  
  
 StdDev = sqrt(p(1-p))  
  
 **连续值**  
  
 存在值 = 1-μ/σ  
  
 不存在值 =-μ/σ  
  
 对值进行编码后，将会对输入进行加权求和，权值为网络边缘。  
  
 对输出的编码使用 Sigmoid 函数，其所具有的特性使其对预测非常有益。 其中一个特性是，无论原始值如何计量，也无论值为正为负，此函数的输出始终在 0 和 1 之间，正好适合于计算概率。 另一个非常有用的特性是，Sigmoid 函数有平滑的效果，值离转折点越远，值的概率会越趋近 0 或 1，但缓慢得多。  
  
## <a name="customizing-the-neural-network-algorithm"></a>自定义神经网络算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法支持多个参数，这些参数可以影响生成的挖掘模型的行为、性能和准确性。 您还可以通过对列设置建模标志来修改模型处理数据的方式，或者通过设置分布标志来指定列中值的处理方式。  
  
### <a name="setting-algorithm-parameters"></a>设置算法参数  
 下表介绍可用于 Microsoft 神经网络算法的参数。  
  
 HIDDEN_NODE_RATIO  
 指定隐藏神经元相对于输入和输出神经元的比率。 以下公式可确定隐藏层中神经元的初始数目：  
  
 HIDDEN_NODE_RATIO * SQRT（总输入神经元 \* 总输出神经元）  
  
 默认值为 4.0。  
  
 HOLDOUT_PERCENTAGE  
 指定定型数据中用于计算维持错误的事例的百分比，定型挖掘模型时的停止条件中将用到此百分比。  
  
 默认值为 30。  
  
 HOLDOUT_SEED  
 指定一个数字，用作在算法随机确定维持数据时伪随机生成器的种子。 如果此参数设置为 0，算法将基于挖掘模型的名称生成种子，以保证重新处理期间模型内容的一致性。  
  
 默认值为 0。  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 确定在应用功能选择前，可应用于算法的输入属性的最大数。 如果将此值设置为 0，则为输入属性禁用功能选择。  
  
 默认值为 255。  
  
 MAXIMUM_OUTPUT_ATTRIBUTES  
 确定在应用功能选择前，可应用于算法的输出属性的最大数。 如果将此值设置为 0，则为输出属性禁用功能选择。  
  
 默认值为 255。  
  
 MAXIMUM_STATES  
 指定算法支持的每个属性的离散状态的最大数。 如果特定属性的状态数大于为该参数指定的数，则算法将使用该属性最普遍的状态并将剩余状态作为缺失的状态处理。  
  
 默认值为 100。  
  
 SAMPLE_SIZE  
 指定用来给模型定型的事例数。 该算法使用此数或 HOLDOUT_PERCENTAGE 参数指定的包含在维持数据中的事例总数的百分比，取两者中较小的一个。  
  
 换言之，如果 HOLDOUT_PERCENTAGE 设置为 30，则该算法将使用此参数的值或事例总数的 70% 的值，取两者中较小的一个。  
  
 默认值为 10000。  
  
### <a name="modeling-flags"></a>建模标志  
 支持将以下建模标志与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法配合使用。  
  
 NOT NULL  
 指示该列不能包含 Null。 如果 Analysis Services 在模型定型过程中遇到 Null 值，将会导致错误。  
  
 适用于挖掘结构列。  
  
 MODEL_EXISTENCE_ONLY  
 指示该模型应仅考虑是否存在属性值或是否缺失值。 不考虑值具体为多少。  
  
 适用于挖掘模型列。  
  
### <a name="distribution-flags"></a>分布标志  
 支持以下分布标志与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法配合使用。 这些标志仅用作对模型的提示；如果算法检测到不同的分布，算法将使用所发现的分布，而不使用提示中提供的分布。  
  
 Normal  
 指示应将列中的值视为表示正态分布（或称高斯分布）。  
  
 Uniform  
 指示应将列中的值视为均匀分布；即，任何值的概率都基本相等，且为值的总数的函数。  
  
 Log Normal  
 指示应将列中的值视为按对数正态曲线分布，即值的对数为正态分布。  
  
## <a name="requirements"></a>要求  
 神经网络模型必须包含至少一个输入列和一个输出列。  
  
### <a name="input-and-predictable-columns"></a>输入列和可预测列  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法支持下表中列出的特定输入列和可预测列。  
  
|“列”|内容类型|  
|------------|-------------------|  
|输入属性|Continuous、Cyclical、Discrete、Discretized、Key、Table 和 Ordered|  
|可预测属性|Continuous、Cyclical、Discrete、Discretized 和 Ordered|  
  
> [!NOTE]  
>  支持 Cyclical 和 Ordered 内容类型，但算法会将它们视为离散值，不会进行特殊处理。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 神经网络算法](microsoft-neural-network-algorithm.md)   
 [神经网络模型的挖掘模型内容&#40;Analysis Services-数据挖掘&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [神经网络模型查询示例](neural-network-model-query-examples.md)  
  
  
