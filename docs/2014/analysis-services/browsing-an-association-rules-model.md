---
title: 浏览关联规则模型 |Microsoft 文档
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining models, browsing
- mining model, association
- mining models, viewing
- association [data mining]
ms.assetid: faffe208-7a64-4ec6-825f-ecbaa79caff7
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4db0b96fe2520a7d9a7aee82ff8d0a3996b730b8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125734"
---
# <a name="browsing-an-association-rules-model"></a>浏览关联规则模型
  当打开关联模型使用**浏览**，在交互式查看器，类似于关联规则查看器中显示该模型[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  此查看器让您能对彼此关联的项一目了然，并显示可用于预测或提出建议的规则。  
  
##  <a name="BKMK_ViewerTabs"></a> 浏览该模型  
 当你打开挖掘模型是使用创建[!INCLUDE[msCoName](../includes/msconame-md.md)]关联规则算法**浏览**窗口包含以下视图，每个主题旨在让您浏览该模型的不同方面：  
  
-   [项集](#BKMK_Itemsets)  
  
-   [规则](#BKMK_Rules)  
  
-   [依赖关系网络](#BKMK_Dependency)  
  
 请记下的在每个选项卡上，选项**显示长名称**。 通过选择此选项，您可以显示或隐藏项集的来源表，并且可以缩短或延长规则或项集的名称。 在事例数据和属性数据来自不同的数据源时，此选项特别有用。  
  
 若要试验关联模型，可使用示例数据工作簿的“关联”选项卡上的示例数据，然后使用所有默认值建立关联模型。 此外可以生成一个购物篮分析模型，并打开该使用**浏览**。  
  
###  <a name="BKMK_Itemsets"></a> 项集  
 **项集**选项卡是开始浏览关联模型的良好开端。 此选项卡列出模型经常发现一起出现的项。  
  
 ![关联模型中项的列表](media/dm13-association-itemsets.gif "关联模型中项的列表")  
  
 最常见的项集示例出现在购物篮模型中，在此模型中，项集表示大量顾客在一次购物中同时购买的产品对或产品集。 不过，根据您分组和排序项的方式，项集可能包含顾客在一段时间内订购的影片序列，或倾向在特定位置发生的事件。  
  
 *项集*可以包含为两个，一项尽可能少三个，或但是，许多被设置为该模型的最大项集大小。 对于每个项集，查看器显示的项集*支持*，*概率*，和*大小*。 支持和概率是用于对关联模型生成的项集和规则进行排名的主要统计信息。 这些值还用于计算和描述项集的重要性。  
  
 **支持**。 支持表示包含此项的事例数或输入数据行数。 例如，如果项集包含两个项都位于一个购物，购物车中中的数字**支持**列指示源数据中发生的项的组合的多少次。  
  
 **大小**。 通过更改项集大小，您可以控制项集列表的长度。 如果你不想要查看单个产品列表中的，更改选项，**最小项集大小**，而 2 或更高。  通过增加项集最小大小来限制列表，您可以查找更为具体的模式。 在处理大型数据集时，这种方法可能很有用。  
  
 你可以筛选项集显示在选项卡中的更改的数目**最小支持**和**最大行**值。 如果你增加**最小支持**值，该列表将显示更少项集，但对项集将输入数据中的较常见的。 常见是否相同为重要的是另一个问题，你可以使用**规则**选项卡。  
  
 请注意该更改的支持值或其他控件上**项集**选项卡只会更改的项的显示，并且不会影响基础模型。 如果你想要生成更少或多个项集，或限制其大小，则应使用参数，`MINIMUM_SUPPORT`和`MAXIMUM_SUPPORT`中的可用**算法参数**对话框。  
  
##### <a name="explore-the-itemsets-list"></a>探索项集列表  
  
1.  单击**支持**列要作为排序依据最高到最低的支持。 这样一来，您可以了解顾客最常购买的商品。  
  
2.  若要专注于特定的项集感兴趣外，许多千位组合, 中键入一些文本**筛选项集**框。  
  
     此处我们键入`Gloves`。 应用此筛选器时，列表将会刷新，仅显示包含手套的项集。 这样一来，您可以重点关注顾客购买手套及其他一些商品的交易。  
  
     **“筛选项集”** 选项还会显示您以前使用过的筛选器列表。  
  
3.  更改的值**最小项集大小**若要筛选出客户购买了只有手套和任何其他项。  
  
4.  单击下拉列表中的选项**显示**，来控制如何显示属性：  
  
    -   **显示属性名称和值**  
  
    -   **仅显示属性值**  
  
    -   **仅显示属性名称**  
  
     请注意名称发生了怎样的变化。 就购物篮模型而言，它是基于多位顾客已购买产品的嵌套表构建的，属性名称通常是产品名称，产品在列表中的存在状态被标记为`Existing`，表示顾客已购买了此物品。  
  
     与`Existing`相反的是`Missing`，后者对于在数据挖掘中开展调查会非常有用。 例如，假设项集 A + B 因此是非常受欢迎你想要查找客户购买项 A，但不是项 b。你无法通过使用预测查询和检索用一个但不是另一个，事务执行此操作，并执行对某些进一步分析。 有关如何在关联模型上创建预测查询的信息，请参阅[关联模型查询示例](data-mining/association-model-query-examples.md)SQL Server 联机丛书中  
  
5.  若要强制以重新显示使用新的筛选条件的项集的列表，你可以选择或清除**显示长名称**复选框。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a> 规则  
 **规则**选项卡将合并项集和其相关值有关的信息。  
  
 ![关联模型所创建的规则的列表](media/dm13-association-rules.gif "关联模型所创建的规则的列表")  
  
 *概率*表示数据集中包含的项目标的组合的情况下的小数部分。 概率是相似的统计概念*置信度*，并提供你的规则的方式可能导致指示即将发生。 您可以更改的值**最小概率**在此窗格中，若要筛选显示的规则。  
  
 值**最小概率**你最初看到的是生成模型时算法使用的阈值。 模型建成后，您无法减小此值，但是可以增大该值以仅显示概率更高的项。  
  
 *重要性*旨在度量规则的用途。 非常常见的规则可能非常普遍，具有很少的信息价值。 重要性越高，则该规则用于预测结果的价值就越高。 在[购物篮分析&#40;for Excel 表 AnalysisTools&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md)工具，可以与项以确定在销售方面可能非常有用的捆绑包的价格组合的重要性。  
  
##### <a name="explore-the-rules-list"></a>探索规则列表  
  
1.  尝试单击列标题-**概率**，**重要性**，和**规则**-若要查看如何在数据发生更改。  
  
2.  使用**筛选规则**选项键入的值并将重点放在目标规则。  
  
     例如，如果您希望查看预测顾客可能会随手套一起购买哪些商品的所有规则，请在文本框中键入“手套”并刷新窗格。  
  
     **“筛选项集”** 选项还会显示您以前使用过的筛选器列表。  
  
3.  若要强制的列表规则以重新显示使用筛选器条件中，你可以选择或清除**显示长名称**复选框。  
  
4.  使用选项，**显示**来控制规则名称的显示方式。  
  
5.  将的值设置**最大行**选项为 100，，然后单击**复制到 Excel**。  
  
     请注意，更改此值对模型中的数据量没有任何影响；它仅控制显示列表中的行数。 在使用特大型模型时，此选项会很有用。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a> 依赖关系网络  
 **依赖关系网络**选项卡是可视的学习路线图的各项之间的相关性。 在图中的每个椭圆 (称为*节点*) 表示一个属性-值对，如"汗衫 = 现有"或"年龄 = 1-30"。  连接椭圆形每个行 (称为*边缘*) 表示的关联类型。  
  
 ![关联模型的依赖关系网络图](media/dm13-association-dependencynetwork.gif "关联模型的依赖关系网络图")  
  
##### <a name="explore-the-dependency-network"></a>探索依赖关系网络  
  
1.  单击**查找**按钮，然后使用**查找节点**对话框中键入感兴趣的项。  
  
     例如，键入“手套”，然后在窗口中最大化图形，以便可以轻松地看到结果。  
  
     包含此项的节点突出显示，指向节点的箭头表示连接项的规则。  
  
     箭头的方向指示规则的方向。 例如，如果购买手套的顾客也可能购买背心，那么箭头将从“手套”节点开始，到“背心”节点终止。  
  
     若要获取有关此规则的其他统计信息，你可以单击**规则**选项卡上和具有描述的规则查找，"手套-现有"->"汗衫 – 现有")  
  
2.  单击并拖动查看器左侧的滑块。  
  
     滑块可作为规则概率的筛选器使用。 降低滑块将只显示最强规则。  
  
3.  单击**复制到 Excel**将当前窗口的快照复制到 Excel。  
  
     你将无法使用你将复制到 Excel 中; 的关系图如果你需要一个交互式网络关系图，使用[查看中的数据挖掘模型 Visio&#40;数据挖掘外接程序&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
## <a name="more-about-association-models"></a>有关关联模型的详细信息  
 你可以使用**浏览**功能可以打开和浏览使用 Microsoft 关联规则算法创建的任何模型。 这包括使用生成的模型[购物篮分析&#40;for Excel 表 AnalysisTools&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md)工具，在**表分析工具**功能区中，或在[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
 如果使用购物篮分析工具创建关联规则模型，则会自动为您配置许多高级选项。  
  
 如果你想要设置高级的参数或更改最小概率和支持，使用[关联向导&#40;for Excel 数据挖掘客户端&#41;](associate-wizard-data-mining-client-for-excel.md)向导中，或生成你自己的模型使用[添加到的模型结构&#40;for Excel 的数据挖掘外接&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)建模选项。  
  
-   **项集：** 在创建模型时，你还可以控制通过将值分配给的 MINIMUM_PROBABILITY 参数生成的项集的数目。 在算法参数对话框中提供了此参数。  
  
-   **规则：** [!INCLUDE[msCoName](../includes/msconame-md.md)]关联规则算法使用概率值来限制的生成的规则数。 可以通过设置 `MINIMUM_PROBABILITY` 或 `MINIMUM _IMPORTANCE` 参数来控制规则数。  
  
 有关配置高级的参数的详细信息，请参阅[数据挖掘算法&#40;SQL Server 数据挖掘外接程序&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md)。  
  
## <a name="see-also"></a>请参阅  
 [浏览 Excel 中的模型&#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  