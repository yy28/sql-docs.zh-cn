---
title: 浏览顺序聚类模型 （数据挖掘中级教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f8a485d5-47ed-4dd5-bb66-ef4d6d463845
caps.latest.revision: 45
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6681bed0736f3927d812dfc0f6beb880aa2fdab3
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313055"
---
# <a name="exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial"></a>浏览顺序分析和聚类分析模型（数据挖掘中级教程）
  现在，已生成**序列聚类分析与地区**模型，你可以浏览它通过使用[!INCLUDE[msCoName](../includes/msconame-md.md)]中序列聚类分析查看器**挖掘模型查看器**数据挖掘设计器选项卡。 [!INCLUDE[msCoName](../includes/msconame-md.md)]序列分类查看器包含五个选项卡：**分类关系图**，**分类剖面图**，**分类特征**， **ClusterDiscrimination**，和**的状态转换**。 有关如何使用此查看器的详细信息，请参阅[使用 Microsoft 序列分类查看器浏览模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)。  
  
-   [群集关系图选项卡上](#bkmk_CDiagram)  
  
-   [群集配置文件选项卡上](#bkmk_CProfiles)  
  
-   [群集特征选项卡上](#bkmk_CChars)  
  
-   [群集对比选项卡上](#bkmk_CDiscrim2)  
  
-   [状态转换选项卡](#bkmk_StateTran)  
  
-   [泛型的内容视图](#bkmk_Generic)  
  
##  <a name="bkmk_CDiagram"></a> 群集关系图选项卡上  
 **分类关系图**选项卡以图形方式显示算法发现的群集数据库中。 关系图中的布局表示分类之间的关系，其中相似的分类分组在一起。 默认情况下，每个节点的明暗度表示分类中所有事例的密度，即节点越暗，它所包含的事例越多。 可以更改节点明暗度代表的含义，使其表示对每个分类内的属性或状态的支持。  
  
 也可以重命名分类，使其更加易于识别并与目标分类结合使用。 在本教程中，您将重命名太平洋地区客户百分比最高的分类，以及事例总数量最多的分类。  
  
> [!NOTE]  
>  在重新处理模型时，分配给特定分类的事例可能会发生更改，具体取决于数据和模型参数。 此外，如果对分类进行了重命名，则在重新处理挖掘模型时，这些名称将会丢失。  
  
#### <a name="to-change-the-attribute-used-for-highlighting-clusters"></a>更改用于突出显示分类的属性  
  
1.  在**明暗度变量**列表中，选择**模型**。  
  
2.  选择**循环 Cap**中**状态**列表。  
  
     该图会进行更新，以显示所选产品在每个分类中的集中度。 最暗的分类包含自行车帽的密度最大。 可以更改明暗度变量，以使用任何输入列的任意状态。  
  
3.  在**明暗度变量**列表中，选择**填充**。  
  
     将明暗度变量更改为客户群体时，该图将进行更新，按大小比较分类。 最暗的分类所包含的事例多于其他分类。  
  
#### <a name="to-rename-nodes-in-the-model"></a>重命名模型中的节点  
  
1.  更改**明暗度变量**到`Region`，并设置**状态**到**太平洋**。  
  
2.  突出显示图形中最暗的节点。  
  
3.  右键单击此群集并选择**重命名群集。**  
  
4.  键入的名称**太平洋群集。**  
  
5.  更改的值**明暗度变量**到**填充**。  
  
6.  在已更新的图形中，找到最暗的分类（应该是最大的分类）。 如果无法通过明暗度来判断哪个分类是最大的，请将鼠标悬停在每个分类上并查看工具提示，然后选择包含事例最多的分类。  
  
7.  右键单击此群集并选择**重命名群集**。 键入新名称， `Largest Cluster`。  
  
 可从表示该分类的节点进行钻取，以查看每个分类中事例的详细信息。 如果要对分析结果进行操作（例如发送电子邮件给客户），则此功能非常有用。 还可以浏览包括在结构中但未在模型中使用的其他一些事例属性，例如 Region 和 IncomeGroup。 有关为基础的情况下从挖掘模型钻取详细信息，请参阅[钻取查询&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
#### <a name="to-drill-through-to-details-from-the-cluster-diagram"></a>从分类关系图钻取到详细信息  
  
1.  右键单击`Pacific Cluster`，选择**钻取**，然后选择**模型和结构列**。  
  
     **钻取**对话框随即打开。 不在模型中使用，但可供查询的列前缀为**结构**。  
  
     可以看到此分类包括的大多数客户都来自太平洋地区，只有少量客户来自其他地区。  
  
2.  单击嵌套列 v Assoc Seq Line Items 中的加号，可以查看特定客户订单中项的顺序。  
  
3.  关闭**钻取**对话框。  
  
    > [!NOTE]  
    >  **播放**按钮使你能够重新查询的数据; 但是，再次查询不会更改的数据显示，除非模型是否已动态更新在后台通过某些其他进程。  
  
 [返回页首](#bkmk_CDiagram)  
  
##  <a name="bkmk_CProfiles"></a> 群集配置文件选项卡上  
 **分类剖面图**选项卡显示每个群集中的序列。 中的右侧的单个列将列出群集**状态**列。  
  
 在查看器中，**模型**行所说明的总体分发情况在群集中，项与**Model.samples**行包含的项的序列。 每个行中的每个单元格的颜色序列**Model.samples**行表示群集中的随机选择用户的行为。  
  
 单个序列直方图中的每一种颜色都代表一个产品型号。 挖掘图例使用颜色编码和产品型号名称来显示产品序列。 如果您已经将其他列添加到聚类分析模型中，例如 Region 或 Income Group，则查看器将包含每个列的附加行，显示这些值在每个分类中的分布。  
  
#### <a name="to-view-the-sequences-that-are-most-common-in-a-cluster"></a>查看分类中最常见的顺序  
  
1.  右键单击**模型**群集列中的行`Largest Cluster`，然后选择**显示图例**。  
  
     **颜色**列包含一个阴影的条，指示在序列中找到的项的频率。 每个项以一种不同颜色表示。 **含义**列列出每种颜色的产品模型名称。 **分发**列告诉您包含该项目在序列中的事例的百分比。  
  
2.  关闭**挖掘图例**。  
  
3.  右键单击**Model.samples**标题、 列中的行**填充**和选择**显示图例**。  
  
4.  扫描的总体模型中的序列的列表`.`  
  
     挖掘图例会首先列出最常见的序列，因此您可以看到 Mountain Tire Tube 是很多序列中的第一项。 这意味着客户很有可能首先将 Mountain Tire Tube 放入购物篮中。  
  
#### <a name="to-drill-through-to-cases-from-the-cluster-viewer"></a>从分类查看器钻取到事例  
  
1.  中向下滚动属性窗格中直到找到所对应的行`Region`属性。  
  
     行包含在模型中，每个群集直方图以及为一个附加的直方图**填充**，这意味着整个集用于在模型中的事例。 直方图是一个带有不同颜色的条，每种颜色代表一个属性，该属性的彩色部分的大小代表了具有该属性的事例的百分比。  
  
2.  比较你重命名的分类直方图`Pacific Cluster`和`Largest Cluster`。 每个分类显示在不同的列中。  
  
     这些颜色看起来都像是纯色，但却是不同的。  
  
3.  在`Region`行中，将鼠标悬停的彩色直方图`Largest Cluster`。  
  
     工具提示将显示一些值，这些值显示了来自每个区域的事例所占的实际百分比。  
  
4.  右键单击彩色的直方图中`Region`行`Pacific Cluster`，选择**钻取**，然后选择**仅限模型列**。  
  
5.  移动滚动条可以查看此分类中的所有客户。  
  
     通过再次钻取到详细信息，可以看到此分类包括的大多数订单都来自太平洋地区，但也有一些订单来自北美和欧洲地区。  
  
6.  关闭**钻取**对话框。  
  
 [返回页首](#bkmk_CDiagram)  
  
##  <a name="bkmk_CChars"></a> 群集特征选项卡上  
 **分类特征**选项卡汇总了通过显示直观地表示所选群集的属性值的重要性的群集中的状态之间的转换。 **变量**列告诉您该模型发现要为所选的分类或填充重要： 特定值或值，称为之间的关系*转换*。 **值**列提供值或转换，有关详细信息和**概率**列以可视方式表示此属性或转换的权重。  
  
#### <a name="to-view-the-important-attributes-for-a-cluster"></a>查看分类的重要属性  
  
1.  在**群集**下拉列表中，选择`Pacific Cluster`。  
  
     列表更新以显示你重命名分类的特征`Pacific Cluster`。 在此群集中，最重要的特征是`Region`。  
  
2.  将鼠标悬停的行中的灰色栏`Region`。  
  
     该值为“Pacific”的概率非常高。 有关如何解释这些值的详细信息，请参阅[Microsoft Sequence Clustering Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)。  
  
3.  仔细查看分类的特征列表，直至找到第一个转换行。  
  
4.  转换行包含转换的文本中**变量**列中和中的顺序的特性值的某些组合**值**列。 该序列也可以包含起点和缺少值。  
  
     例如，假定转换的值为 [Start] -> Road Tire Tube。 这意味着此分类中的客户通常首先将 Road Tire Tube 放入购物篮中。 这可能表示该产品是客户首先挑选出的受欢迎商品，或者只表示该产品在购物场所容易找到。  
  
5.  滚动，直到找到没有的第一个转换列表 **[入门]** 或**缺少**中它。  
  
     例如，假设你发现该项过渡，**旅行车轮胎、 旅行车轮胎管**。 这意味着此分类中的客户通常将这些项一起放入购物篮中，而且是严格按照这个顺序放入。  
  
6.  将鼠标悬停在此转换的阴影条上。  
  
     此转换的概率以百分比显示。  
  
7.  在**群集**下拉列表中，选择**总体 （全部）**。  
  
     该属性列表会更新为显示用于创建模型的所有订单的特征。 在此挖掘模型中，以区分群集之间的最重要特征是`Region`，值为**北美**。  
  
 在查看这些任务后，您认识到两点。 第一点是您需要大量数据来获取有意义数量的组合。 例如，具有最高概率的序列是可能包括 **[入门]** 或**缺少**状态。  
  
 第二个是很强的聚类分析的属性影响`Region`，这样就更加困难，若要查看的序列组。 因此，您决定创建另一个模型，该模型只使用序列，而且不包括区域或收入的列。  
  
 [返回页首](#bkmk_CDiagram)  
  
##  <a name="bkmk_CDiscrim2"></a> 群集对比选项卡上  
 **分类对比**选项卡可以帮助你比较两个分类，以确定哪些属性将特定群集与另一个群集区分开来。 该选项卡包含四列：**变量**，**值**，**群集 1**，和**群集 2**。  你可以选择要用作任何群集**群集 1**和**群集 2**。  
  
 **变量**列会告诉您的属性，它可以是列名称或列名称和该单词的组合姓名**转换**。 **值**列显示属性或转换的确切值。 中的列的灰色的栏**群集 1**和**群集 2**指示要比较的群集中的属性的强度。 阴影条越长，分类包括具有该属性的事例的可能性越大。  
  
#### <a name="to-compare-two-clusters-by-using-the-cluster-discrimination-tab"></a>使用“分类对比”选项卡比较两个分类  
  
1.  在**分类对比**选项卡上，为**群集 1**，选择`Pacific Cluster`。  
  
     默认情况下，所选择的**群集 2**更改为**太平洋补数 * * * 群集**。  
  
     最上面的属性，用于区分`Pacific Cluster`从所有其他情况下是的区域。 Region 是聚类分析的一个强属性，以至于它掩盖了其他属性。 为了避免这种效果，请尝试相互比较几个较小的分类。 在进行比较时，属性列表会发生变化，可能包括模型之间的更多转换。  
  
2.  找到转换行，将鼠标悬停在阴影条上。  
  
     中的项**值**列可以包括状态和转换。 各项的明暗度指示对比分数。 若要了解有关不同分数的含义的详细信息，请参阅[挖掘模型内容的序列聚类分析模型&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)。  
  
 [返回页首](#bkmk_CDiagram)  
  
##  <a name="bkmk_StateTran"></a> 状态转换选项卡  
 上**状态转换**选项卡上，你可以选择一个分类，并浏览其状态转换。 如果你选择**总体 （全部）** 从群集下拉列表中，关系图显示针对整个挖掘模型的状态分布。  
  
 图中的每个节点都表示一个状态，或您试图分析的序列的可能值。 节点的背景色表示该状态的频率。 一些状态之间用线条连接，指示这些状态之间的转换。 可以上下移动滑块，以更改转换的概率阈值。 数字与某些节点相关联，指示该状态的概率。  
  
#### <a name="to-explore-the-relationships-in-the-state-transition-tab"></a>在“状态转换”选项卡中浏览关系  
  
1.  在**状态转换**的挖掘模型查看器中，选择的选项卡`Pacific Cluster`从群集的列表。 确保**显示边缘标签**选项。  
  
     该图会更新为显示此分类中最常见的转换。  
  
2.  单击通过线条连接到另一个节点的任何节点。  
  
     该图进行了更新，并且突出显示相关的节点。 线条旁的数值指示转换的概率。  
  
3.  最多引发滑块**所有链接**，以增加在图中包含的转换数。  
  
4.  选择**总体 （全部）** 从**群集**。  
  
     请注意，在加载另一个分类时，该图会重置为默认显示设置，因此滑块控件也会重置到中间位置。  
  
5.  单击关系图，它应该是中的最深节点**运动 100**。  
  
     请注意，产品之间没有线条相互连接。  
  
6.  将滑块向上提升一级，以增加图中包括的转换的数量。 不会一直到**所有链接**尚未。  
  
     该图会添加更多的转换，从而进行更新，但这些转换都没有包括 Sport-100 型号。  
  
7.  移动滑块控制一直到**所有链接**。 如果尚未选择 Sport-100 节点，请单击该节点。  
  
     该图会更新为显示包括 Sport-100 产品的很多转换。 连接线条的箭头的方向指示 Sport-100 项是作为配对中的第一项还是第二项选择的。  
  
8.  单击 Touring Tire 的节点，将滑块控件向下移回至中间位置。  
  
     开始时，有很多将 Touring Tire 与其他产品连接起来的转换线，但当您提高概率阈值时，可能性较低的转换就不再显示在图中，只剩下转换 Touring Tire > Touring Tire Tube。 此转换的含义是如果客户将 Touring Tire 放入购物篮，则该客户接下来将 Touring Tire Tube 也放入购物篮的概率非常高。  
  
 [返回页首](#bkmk_CDiagram)  
  
##  <a name="bkmk_Generic"></a> 一般内容树查看器  
 此查看器可用于所有模型，无论算法和模型类型为何均为如此。 **MicrosoftGeneric 内容树查看器**可从**查看器**下拉列表。  
  
 内容树是任何挖掘模型的表示形式，由一系列节点组成，其中每个节点都表示关于定型数据的已了解的知识。 节点可以包含一种模式、一组规则、一个分类或共享某些属性的日期范围的定义。 根据算法和可预测属性的不同，节点的具体内容会有所不同，但内容的通用表示形式是相同的。  
  
 您可以展开每个节点以查看详细信息的递增级别，并可以将任何节点的内容复制到剪贴板。 有关详细信息，请参阅 [使用 Microsoft 一般内容树查看器浏览模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)。  
  
#### <a name="to-view-details-for-a-sequence-clustering-model-by-using-the-generic-content-tree-viewer"></a>使用一般内容树查看器查看顺序分析和聚类分析模型的详细信息  
  
1.  在**挖掘模型查看器**选项卡上，单击**查看器**列表，然后选择**Microsoft 一般内容树查看器**。  
  
2.  在**节点标题**窗格中，单击`Pacific Cluster (1)`。  
  
     此节点的名称同时包含为分类指定的友好名称和基础节点 ID。 可以使用节点 ID 来深化到模型中的其他详细信息。  
  
3.  展开第一个子节点中，名为**分类 1 的序列级别**。  
  
     分类的序列级别节点包含了关于该分类中的状态和转换的详细信息。 可以使用 NODE_DISTRIBUTION 列中的这些详细信息，浏览每个节点或模型的序列和状态。  
  
4.  继续展开节点并在 HTML 查看器窗格中查看详细信息。  
  
 有关挖掘模型内容，以及如何查看器中使用的详细信息的详细信息，请参阅[序列聚类分析模型的挖掘模型内容&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)。  
  
 [返回页首](#bkmk_CDiagram)  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建相关的序列聚类分析模型&#40;中间数据挖掘教程&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [Microsoft Sequence Clustering Algorithm](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [顺序分析和聚类分析模型查询示例](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)  
  
  