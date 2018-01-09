---
title: "MDX (Analysis Services) 中的重要概念 |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], about MDX
- dimensional modeling [MDX]
- MDX [Analysis Services], about MDX
- Multidimensional Expressions [Analysis Services], dimensional modeling
- MDX [Analysis Services], dimensional modeling
ms.assetid: 4797ddc8-6423-497a-9a43-81a1af7eb36c
caps.latest.revision: "52"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 23aca9e6a5595c8597d13e2e832390988c50be3c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="key-concepts-in-mdx-analysis-services"></a>MDX 中的重要概念 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]你可以使用多维表达式 (MDX) 查询多维数据，或者创建多维数据集中的 MDX 表达式之前，它有助于了解多维概念和术语。  
  
 最好从已了解的数据汇总示例开始，然后查看 MDX 如何与之相关。 这是一个在 Excel 中创建的数据透视表，由 Analysis Services 示例多维数据集中的数据填充。  
  
 ![数据透视表的度量值和维度调出](../../../analysis-services/multidimensional-models/media/ssas-keyconcepts-pivot1-measures-dimensions.png "的度量值和维度调出的数据透视表")  
  
## <a name="measures-and-dimensions"></a>度量值和维度  
 Analysis Services 多维数据集包含度量值、维度和维度属性，所有这些在数据透视表示例中都显而易见。  
  
 **度量值** 是单元格中聚合为总和、计数、百分比、最小值、最大值或平均值的数值数据值。 度量值是实时计算出的动态值，响应用户导航并与数据透视表交互。 在本示例中，单元格显示根据轴是否展开或折叠而增加或减少的“分销商销售额”。 对于“日期”（年份、季度、月份或日期）和“销售区域”（国家/地区分组、国家/地区、区域）的任意组合，都可获得为特定上下文求和的“分销商销售额”。 与度量值同义的其他术语包括事实数据（位于数据仓库中）和计算字段（位于表格和 Excel 数据模型中）。  
  
 **维度** 位于数据透视表的列和行轴上，提供度量值背后的含义。 维度类似于关系数据模型中的表。 维度的常见示例包括“时间”、“地域”、“产品”、“客户”和“员工”等。 此示例包含两个维度，即行上的“销售区域”和横跨顶部的“日期”，但可以很容易地拖放与“分销商销售额”关联的其他维度（例如“促销”或“产品”），从而按这些维度查看销售业绩。 以有趣的方式浏览数据的能力取决于创建的维度，以及这些维度是否与数据源中的事实数据表相关。  
  
 **维度属性** 是维度中的命名项，类似于表中的列。 在本示例中，“销售区域”维度属性包含“国家/地区分组”（欧洲、北美和太平洋地区）、“国家/地区”（加拿大、美国）以及“区域”（中部、东北、西北、东南和西南）。  
  
 每个属性都具有与其关联的数据值或成员的集合。 在我们的示例中，“国家/地区分组”属性的成员包括欧洲、北美和太平洋地区。 **成员** 表示属于某个属性的实际数据值。  
  
> [!NOTE]  
>  数据建模的一个方面就是形式化数据本身已包含的模式和关系。 处理自然层次结构中的数据时，与国家/地区-区域-城市的情况一样，可通过创建一个 **属性关系**来形式化该关系。 “属性关系”是属性间的一对多关系，例如州（省市自治区）和城市间的关系 – 一个州（省市自治区）有多个城市，而一个城市只能属于一个州（省市自治区）。 在模型中创建属性关系可加速查询性能，因此最好在数据支持的情况下创建属性关系。 可在 SQL Server Data Tools 中的维度设计器中创建属性关系。 请参阅 [Define Attribute Relationships](../../../analysis-services/multidimensional-models/attribute-relationships-define.md)。  
  
 Excel 中的模型元数据显示在数据透视表字段列表中。  将上面的数据透视表与下面的字段列表进行比较。 注意，字段列表包含“销售区域”、“组”、“国家/地区”和“区域”（元数据），而数据透视表仅包含成员（数据值）。 了解图标的样子有助于轻松地将部分多维模型与 Excel 中的数据透视表关联起来。  
  
 ![数据透视表字段列表](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-ptfieldlist.png "数据透视表字段列表")  
  
## <a name="attribute-hierarchies"></a>属性层次结构  
 几乎不用思考即可知道数据透视表中的值会随着展开或折叠每个轴的级别增加或减少，但原因何在？ 答案在于属性层次结构。  
  
 折叠所有级别，注意每个“国家/地区分组”和“日历年”的总计。 此值由层次结构中的 **“(全部)”成员** 派生而来。 “(全部)”成员是属性层次结构中所有成员的计算值。  
  
-   所有“国家/地区分组”和“日期”的“(全部)”成员总和为 $80,450,596.98  
  
-   CY2008 的“(全部)”成员为 $16,038,062.60  
  
-   “太平洋地区”的“(全部)”成员为 $1,594,335.38  
  
 像这样的聚合是预先计算并提前存储好的，这就是 Analysis Services 快速查询性能的秘密之一。  
  
 ![具有标注的所有成员的数据透视表](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-pivot2-allmember.png "调出的所有成员包含数据透视表")  
  
 展开层次结构，最终会看到最低级别。 这称为 **叶成员**。 叶成员是层次结构中不包含子级的成员。 在此示例中，“澳大利亚”是叶成员。  
  
 ![包含叶成员杨柳 dout 数据透视表](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-pivot3-leafparent.PNG "包含叶成员杨柳 dout 数据透视表")  
  
 其上的任何成员称为 **父成员**。 “太平洋地区”是“澳大利亚”的父级。  
  
 **属性层次结构的组件**  
  
 所有这些概念共同构建出 **属性层次结构**的概念。 属性层次结构是包含以下级别的属性成员的树形结构：  
  
-   包含所有非重复属性成员的叶级别，叶级别的各个成员也称为 **叶成员**。  
  
-   中间级别（如果属性层次结构为父子层次结构）（稍后将详细介绍）。  
  
-   包含所有子属性的聚合值的“(全部)”成员。 此外，还可以选择在“(全部)”级别不适用于数据时可将其隐藏或关闭。 例如，虽然“产品代码”是数字，但对所有“产品代码”求和、计算其平均数或进行其他方式的聚合是没有意义的。  
  
> [!NOTE]  
>  BI 开发人员经常设置属性层次结构的属性，以实现客户端应用程序的某些行为，或获得某些性能优势。 例如，可针对属性设置 AttributeHierarchyEnabled=False，此时“(全部)”成员没有意义。 或者，可能只是想隐藏“(全部)”成员，此时可设置 AttributeHierarchyVisible=False。 有关属性的详细信息，请参阅 [Dimension Attribute Properties Reference](../../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md) 。  
  
## <a name="navigation-hierarchies"></a>导航层次结构  
 在数据透视表中（至少在本实例中），展开行和列轴以显示较低级别的属性。 可展开的树形结构是通过模型中创建的导航层次结构实现的。  在 AdventureWorks 示例模型中，“销售区域”维度包含以“国家/地区分组”开头、后面依次为“国家/地区”和“区域”的多级层次结构。  
  
 正如您所看到的，层次结构用于在数据透视表或其他数据汇总对象中提供导航路径。 有两种基本类型：均衡层次结构和不均衡层次结构。  
  
 **均衡层次结构**  
  
|||  
|-|-|  
|![具有标注的平衡层次结构的数据透视表](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-pivot4-balancedhierarchy.PNG "调出的均衡层次结构包含数据透视表")|**均衡层次结构** 是顶级成员与任何叶成员之间存在相同级别数的层次结构。<br /><br /> **自然层次结构** 是从基础数据中自然产生的层次结构。 常见的示例是“国家/地区-区域-城市”、“年-月-日”或“类别-子类别-模型”，每个从属级别都以可预测的方式从父级中流出。<br /><br /> 在多维模型中，大多数层次结构都是均衡层次结构，其中许多也属于自然层次结构。<br /><br /> 另一个相关的建模术语是 **用户定义的层次结构**，该术语常用于与属性层次结构形成对比。 它仅仅表示由 BI 开发人员创建的层次结构，与 Analysis Services 在您定义属性时自动生成的属性层次结构相反。|  
  
 **不均衡层次结构**  
  
|||  
|-|-|  
|![具有标注的不规则层次结构的数据透视表](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-pivot15-raggedhierarchy.PNG "调出的不规则层次结构包含数据透视表")|**不规则层次结构** 或 **不均衡层次结构** 是顶级与叶成员之间存在不同级别数的层次结构。 同样，这也是由 BI 开发人员创建的层次结构，但在这种情况下数据中存在间隔。<br /><br /> 在 AdventureWorks 示例模型中，“销售区域”阐释了不规则层次结构，因为在本示例中，美国具有其他国家/地区不存在的额外的级别 (“区域”)。<br /><br /> 如果客户端应用程序不能以较好的方式来处理不规则层次结构，则该层次结构对于 BI 开发人员是一个挑战。 在 Analysis Services 模型中，可以创建一个显式定义多级别数据间的关系的 **父子层次结构** ，以便消除一个级别与下一个级别的关联方式的不明确性。 有关详细信息，请参阅 [父子维度](../../../analysis-services/multidimensional-models/parent-child-dimension.md) 。|  
  
## <a name="key-attributes"></a>键属性  
 模型是依赖键和索引进行关联的相关对象的集合。 Analysis Services 模型也是如此。 每个维度（等同于关系模型中的表）均存在一个键属性。 **键属性** 用于事实数据表（度量值组）的外键关系。 维度中的所有非键属性均（直接或间接）链接至键属性。  
  
 键属性通常是（但并非总是） **粒度属性**。 粒度是指数据内详细信息的级别或精度的级别。 同样，常见示例为理解相关内容提供最快的途径。 考虑日期值：对于日常销售，需要按天指定的日期值；对于配额，只需按季度即可，但如果分析数据包含体育事件的比赛结果，则粒度最好为毫秒。 粒度就是数据值的精度级别。  
  
 另一个示例是货币：财务应用程序跟踪货币值时可能会精确到多位小数位数，而本地学校基金筹集可能只需最接近美元的值。 因为想要避免存储不必要的数据，所以了解粒度非常重要。 删除时间戳中的毫秒或销售额中的分可在该详细信息级别与分析无关时节省存储和处理时间。  
  
 若要设置粒度属性，请使用 SQL Server Data Tools 中多维数据集设计器的“维度用法”选项卡。 在 AdventureWorks 示例模型中，“日期”维度的键属性是“日期”键。 对于“销售订单”，粒度属性等同于键属性。 对于“销售目标”，粒度级别是季度，因此粒度属性相应地设置为“日历季度”。  
  
 ![模型显示粒度属性](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-granularityattrib.png "模型显示粒度属性")  
  
> [!NOTE]  
>  如果粒度属性与键属性不同，则所有非键属性都必须直接或间接地链接到粒度属性。 在多维数据集中，粒度属性定义维度的粒度。  
  
## <a name="query-scope-cube-space"></a>查询范围（多维数据集空间）  
 查询范围是指选择数据的边界。 其范围可从整个多维数据集（多维数据集是最大的查询对象）到一个单元格。  
  
 **多维数据集范围** 是多维数据集属性层次结构的成员与多维数据集的度量值的乘积。  
  
 **子多维数据集** 是表示多维数据集的筛选视图的多维数据集子集。 可以使用 MDX 计算脚本中的 Scope 语句，或在 MDX 查询中的嵌套 select 语句中定义子多维数据集，或者定义为会话多维数据集。  
  
 **单元格** 是指度量值维度成员的成员与多维数据集中各个属性层次结构的成员相交处所在的空间。  
  
## <a name="other-modeling-terms"></a>其他建模术语  
 本节介绍一系列不太适合其他章节，但仍需了解的概念和术语。  
  
 **计算成员** 是在查询时间定义和计算的维度成员。 可以在用户查询或 MDX 计算脚本中定义计算成员，并将其存储在服务器上。 一个计算成员对应于定义该成员的维度中的多个维度表行。  
  
 **非重复计数** 是用于只应计数一次的数据项的一种特殊的度量值。 AdventureWorks 示例模型包括针对“Internet 订单”、“分销商订单”和“销售订单”的非重复计数度量值。  
  
 **度量值组** 是一个或多个度量值的集合。 其中大多数度量值组是用户定义的，可用于将相关度量值保留在一起。 非重复计数度量值是一个例外。 非重复计数度量值始终置于仅包含非重复度量值的专用度量值组中。 该度量值组不会显示在数据透视表示例中，但会作为度量值的命名集合显示在数据透视表字段列表中。  
  
 **度量值维度** 是包含多维数据集中所有度量值的维度。 它不会在 SQL Server Data Tools 中生成的多维模型中显示，但它仍然存在。 度量值维度包含度量值，因此它的所有成员通常都是聚合的（通常采用求和或计数方式）。  
  
 **数据库维度和多维数据集维度**。 可以在模型中定义独立的维度，该维度之后将包含在同一模型中任意数量的多维数据集中。 将维度添加到多维数据集时，该维度被称为多维数据集维度。 作为对象资源管理器中的独立项单独存在于项目中时，该维度被称为数据库维度。 为什么要进行区别？ 因为这样可以单独设置其属性。 在产品维度中，您将看到两个术语都有使用，因此值得了解其各自的含义。  
  
## <a name="next-steps"></a>Next Steps  
 现在，您已掌握重要的概念和术语，可以继续了解这些进一步阐述 Analysis Services 中的基本概念的附加主题：  
  
-   [基本 MDX 查询 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)  
  
-   [基本 MDX 脚本 (MDX)](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)  
  
-   [多维建模（Adventure Works 教程）](../../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [Cube Space](../../../analysis-services/multidimensional-models/mdx/cube-space.md)   
 [元组](../../../analysis-services/multidimensional-models/mdx/tuples.md)   
 [Autoexists](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [使用成员、元组和集 (MDX)](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [直观合计和非直观合计](../../../analysis-services/multidimensional-models/mdx/visual-totals-and-non-visual-totals.md)   
 [MDX 查询基础知识 &#40;Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [MDX 脚本编写基础知识 &#40;Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [MDX 语言参考 (MDX)](../../../mdx/mdx-language-reference-mdx.md)   
 [多维表达式 (MDX) 参考](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
