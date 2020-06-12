---
title: 浏览关联规则模型 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining model, association
- mining models, viewing
- association [data mining]
ms.assetid: faffe208-7a64-4ec6-825f-ecbaa79caff7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 69002d17205a5631d555e1022b8adeb9e51d3db2
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527728"
---
# <a name="browsing-an-association-rules-model"></a>浏览关联规则模型
  使用 "**浏览**" 打开关联模型时，该模型将显示在交互式查看器中，类似于中的关联规则查看器 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。  此查看器让您能对彼此关联的项一目了然，并显示可用于预测或提出建议的规则。  
  
##  <a name="explore-the-model"></a><a name="BKMK_ViewerTabs"></a>浏览模型  
 当您打开使用关联规则算法创建的挖掘模型时 [!INCLUDE[msCoName](../includes/msconame-md.md)] ，"**浏览**" 窗口包括以下视图，每个视图都允许您浏览模型的不同方面：  
  
-   [项集](#BKMK_Itemsets)  
  
-   [规则](#BKMK_Rules)  
  
-   [依赖关系网络](#BKMK_Dependency)  
  
 记下每个选项卡上的选项 "**显示长名称**"。 通过选择此选项，您可以显示或隐藏项集的来源表，并且可以缩短或延长规则或项集的名称。 在事例数据和属性数据来自不同的数据源时，此选项特别有用。  
  
 若要试验关联模型，可使用示例数据工作簿的“关联”选项卡上的示例数据，然后使用所有默认值建立关联模型。 你还可以使用 "**浏览**" 来构建购物篮分析模型并打开它。  
  
###  <a name="itemsets"></a><a name="BKMK_Itemsets"></a>项集  
 "**项集**" 选项卡是开始浏览关联模型的好地方。 此选项卡列出模型经常发现一起出现的项。  
  
 ![关联模型中项的列表](media/dm13-association-itemsets.gif "关联模型中项的列表")  
  
 最常见的项集示例出现在购物篮模型中，在此模型中，项集表示大量顾客在一次购物中同时购买的产品对或产品集。 不过，根据您分组和排序项的方式，项集可能包含顾客在一段时间内订购的影片序列，或倾向在特定位置发生的事件。  
  
 一个*项集只能包含*一项到两个、三个或多个项，也可以将多个项设置为该模型的最大项集大小。 对于每个项集，查看器将显示项集的*支持*、*概率*和*大小*。 支持和概率是用于对关联模型生成的项集和规则进行排名的主要统计信息。 这些值还用于计算和描述项集的重要性。  
  
 **支持**。 支持表示包含此项的事例数或输入数据行数。 例如，如果项集包含在购物车中找到的两个项，则 "**支持**" 列中的数字指示在源数据中发生项组合的次数。  
  
 **大小**。 通过更改项集大小，您可以控制项集列表的长度。 如果不想看到列表中的单个产品，请将选项 "**最小**项集大小" 更改为2或更大。  通过增加项集最小大小来限制列表，您可以查找更为具体的模式。 在处理大型数据集时，这种方法可能很有用。  
  
 可以通过更改 "**最低支持**" 和 "**最大行**数" 值来筛选选项卡中显示的项集的数目。 如果增加**最小支持**值，列表将显示较少的项集，但项集将是输入数据中更常见的值。 与 "重要" 是否相同是 "重要" 是另一个问题，你可以使用 "**规则**" 选项卡浏览。  
  
 请注意，更改 "**项集**" 选项卡上的支持值或其他控件仅更改显示的项，而不会影响基础模型。 如果要生成更少或更多的项集或限制其大小，应使用 `MINIMUM_SUPPORT` `MAXIMUM_SUPPORT` "**算法参数**" 对话框中提供的参数和。  
  
##### <a name="explore-the-itemsets-list"></a>探索项集列表  
  
1.  单击 "**支持**" 列以便按最高到最低的支持排序。 这样一来，您可以了解顾客最常购买的商品。  
  
2.  若要将重点放在可能的一个或多个组合中，请在 "**筛选**项集" 框中键入一些文本。  
  
     这里，我们键入了 `Gloves` 。 应用此筛选器时，列表将会刷新，仅显示包含手套的项集。 这样一来，您可以重点关注顾客购买手套及其他一些商品的交易。  
  
     **“筛选项集”** 选项还会显示您以前使用过的筛选器列表。  
  
3.  更改 "**最小**项集大小" 的值，以筛选出仅购买了手套而不是其他商品的客户。  
  
4.  单击 "**显示**" 选项的下拉列表以控制属性的显示方式：  
  
    -   **显示属性名称和值**  
  
    -   **仅显示属性值**  
  
    -   **仅显示属性名称**  
  
     请注意名称发生了怎样的变化。 就购物篮模型而言，它是基于多位顾客已购买产品的嵌套表构建的，属性名称通常是产品名称，产品在列表中的存在状态被标记为`Existing`，表示顾客已购买了此物品。  
  
     与`Existing`相反的是`Missing`，后者对于在数据挖掘中开展调查会非常有用。 例如，假设项集 A + B 非常受欢迎，希望查找购买项 A 但不是项 B 的客户。为此，您可以使用预测查询并检索其中一个事务，而不是另一个事务，并对这些事务进行进一步的分析。 有关如何创建针对关联模型的预测查询的信息，请参阅 SQL Server 联机丛书中的[关联模型查询示例](data-mining/association-model-query-examples.md)  
  
5.  若要强制使用新筛选条件重新显示项集列表，可以选中或清除 "**显示长名称**" 复选框。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
###  <a name="rules"></a><a name="BKMK_Rules"></a>原则  
 "**规则**" 选项卡将有关项集及其相对值的信息合并在一起。  
  
 ![关联模型创建的规则列表](media/dm13-association-rules.gif "关联模型创建的规则列表")  
  
 *概率*表示包含目标组合项的数据集中的事例部分。 "概率" 类似于 "*置信度*" 的统计概念，并提供了有关如何发生规则结果的指示。 可以在此窗格中更改 "**最小概率**" 的值，以筛选所显示的规则。  
  
 最初看到的**最小概率**值是在生成模型时算法使用的阈值。 模型完成后，你将无法减少此值，但你可以将其增大到仅显示更高概率项。  
  
 *重要性*用于度量规则的有用性。 非常常见的规则可能非常普遍，具有很少的信息价值。 重要性越高，则该规则用于预测结果的价值就越高。 在[购物篮分析 &#40;表 AnalysisTools For Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)工具中，重要性可以与商品价格结合，以确定在销售方面可能最有价值的捆绑包。  
  
##### <a name="explore-the-rules-list"></a>探索规则列表  
  
1.  尝试单击列标题 "**概率**"、"**重要性**" 和 "**规则**" 以查看数据更改的方式。  
  
2.  使用 "**筛选规则**" 选项可以键入值并专注于目标规则。  
  
     例如，如果想要查看预测哪些客户可能与手套一起购买的所有规则，请在文本框中键入 "手套" 并刷新窗格。  
  
     **“筛选项集”** 选项还会显示您以前使用过的筛选器列表。  
  
3.  若要强制使用筛选条件重新显示规则列表，可以选中或清除 "**显示长名称**" 复选框。  
  
4.  使用选项 "**显示**" 以控制规则名称的显示方式。  
  
5.  将 "**最大行数**" 选项的值设置为100，然后单击 "**复制到 Excel**"。  
  
     请注意，更改此值不会对模型中的数据量产生任何影响;它只控制显示列表中的行数。 在使用特大型模型时，此选项会很有用。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
###  <a name="dependency-network"></a><a name="BKMK_Dependency"></a>依赖关系网络  
 "**依赖关系网络**" 选项卡是项之间的关联的可视化地图。 图形中的每个椭圆（称为*节点*）表示一个属性-值对，如 "背心 = 现有" 或 "Age = 1-30"。  连接椭圆（称为*边缘*）的每行表示一种相关性。  
  
 ![关联模型的依赖关系网络图形](media/dm13-association-dependencynetwork.gif "关联模型的依赖关系网络图形")  
  
##### <a name="explore-the-dependency-network"></a>探索依赖关系网络  
  
1.  单击 "**查找**" 按钮，然后使用 "**查找节点**" 对话框键入感兴趣的项。  
  
     例如，键入 "手套"，然后在窗口中最大化图形，以便您可以轻松地看到结果。  
  
     包含此项的节点突出显示，指向节点的箭头表示连接项的规则。  
  
     箭头的方向指示规则的方向。 例如，如果购买了手套的人员也可能购买背心，箭头将从 "手套" 节点开始，并在 "背心" 节点上终止。  
  
     若要获取有关此规则的附加统计信息，可以单击 "**规则**" 选项卡，然后查找描述为 "手套"-> "背心"）的规则。  
  
2.  单击并拖动查看器左侧的滑块。  
  
     滑块可作为规则概率的筛选器使用。 降低滑块将只显示最强规则。  
  
3.  单击 "**复制到 excel** "，将当前窗口的快照复制到 excel。  
  
     无法使用复制到 Excel 中的图形。如果需要交互式网络图形，请使用在[Visio 中查看数据挖掘模型 &#40;数据挖掘外接程序&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
## <a name="more-about-association-models"></a>有关关联模型的详细信息  
 您可以使用 "**浏览**" 功能打开并浏览使用 Microsoft 关联规则算法创建的任何模型。 这包括使用[购物篮分析 &#40;Table AnalysisTools For Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)工具、**表分析工具**功能区中或中生成的模型 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。  
  
 如果使用购物篮分析工具创建关联规则模型，则会自动为您配置许多高级选项。  
  
 如果要设置高级参数或更改最小概率和支持，请使用[关联向导 &#40;excel&#41;的数据挖掘客户端](associate-wizard-data-mining-client-for-excel.md)"向导，或使用"[将 &#40;用于 Excel 的数据挖掘外数据挖掘外接程序&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)建模 "选项构建你自己的模型。  
  
-   **项集：** 创建模型时，还可以通过向 MINIMUM_PROBABILITY 参数赋值来控制生成的项集的数目。 此参数可从“算法参数”对话框中获得。  
  
-   **规则：**[!INCLUDE[msCoName](../includes/msconame-md.md)]关联规则算法使用概率值来限制所生成的规则数。 可以通过设置 `MINIMUM_PROBABILITY` 或 `MINIMUM _IMPORTANCE` 参数来控制规则数。  
  
 有关配置高级参数的详细信息，请参阅[&#40;SQL Server 数据挖掘外接程序&#41;的数据挖掘算法](data-mining-algorithms-sql-server-data-mining-add-ins.md)。  
  
## <a name="see-also"></a>另请参阅  
 [在 Excel 中浏览模型 &#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
