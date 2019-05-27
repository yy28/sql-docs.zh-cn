---
title: 关联向导 （数据挖掘客户端 Excel） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- nested tables, in association models
- association [data mining]
ms.assetid: 4db6462f-93c7-443f-8ff7-39474dc7029e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 15a86cc55e67b2000eabee62d02fa04de4874f59
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062306"
---
# <a name="associate-wizard-data-mining-client-for-excel"></a>关联向导（Excel 数据挖掘客户端）
  ![数据挖掘功能区中的关联向导](media/dmc-associate.gif "数据挖掘功能区中的关联向导")  
  
 关联向导可以帮助您使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联规则算法来创建数据挖掘模型。 这样的挖掘模型是用于创建特别有用*推荐系统*。  
  
 其工作方式为 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联规则算法扫描由事务或事件组成的数据集，然后找到经常一起出现的组合。 可能有数千个组合，但是，可自定义该算法以查找更多或更少以及仅保留最有可能的组合。  
  
 可将关联分析应用于许多问题。 此方法的最常见的应用是购物篮分析，该分析可找到经常一起购买的个别产品。 然后，您可以使用这些信息根据客户已经购买的物品向其推荐产品。  
  
## <a name="using-the-associate-wizard"></a>使用关联向导  
  
1.  在中**数据挖掘**功能区中，单击**关联**。  
  
2.  上**选择数据源**页上，选择 Excel 表或数据区域，然后单击**下一步**。  
  
     示例数据工作簿的“关联”选项卡中包含一个示例，说明每笔交易中有多个产品或每个客户有多个采购记录时，交易数据通常的排列方式。  
  
     如果你想要使用外部数据生成关联模型使用关联向导，您必须将数据添加到 Excel 第一次，并*平展*数据。 为关联建模准备数据的详细信息，请参阅[嵌套表&#40;Analysis Services-数据挖掘&#41;](data-mining/nested-tables-analysis-services-data-mining.md)，在 SQL Server 联机丛书。  
  
3.  上**关联**页上，选择标识交易的列。  
  
     对于购物篮模型，此标识符表示要建模的单元。 您是要分析单个客户一段时间内购买的物品，还是要分析涉及多个客户的多宗交易？ 在第一种情况下，您可以选择客户 ID；在后一种情况下，您可以选择采购订单或其他交易 ID。  
  
4.  有关**项**，选择包含您需要在其中查找关联的内容的列。  
  
     例如，在购物篮模型中，您可以选择一个产品字段以分析哪些产品通常会被一起购买。 如果要有效关联在一起的单个产品数量过多，可以选择一个产品类别或子类别字段。  
  
5.  在中**阈值**，可以设置用于控制或影响模型的输出值：  
  
    -   **最小支持。** 指定一组项目要被视为重要必须达到的出现次数。 此算法将忽略任何不满足此条件的项组合。 例如，您可能希望仅看到整体一起出现至少 10 次的项集。  
  
    -   **最小规则概率**。 指定使规则得以保存所需的最小概率值。 分析整个数据集以找出所有组合，然后计算出概率。 如果该阈值过低，则向导可能会将关联度较低的项关联在一起。 如果该阈值过高，则某些关联将可能会被忽略，因为它们没有足够的支持数据。  
  
     一般来说，更改这些值将产生以下影响：  
  
    -   如果减小支持的值，则会增加找到的组合数。  
  
    -   如果减小最大支持，则会筛选出因频繁出现而没有多少意义的项。  
  
    -   如果降低规则的概率，则会降低组合在整个数据集上下文中被视为重要组合所必须满足的要求。  
  
     **提示：** 它是创建使用支持和概率的不同组合的多个挖掘模型的一个好办法。 若要跟踪对每个模型使用了哪些设置，可以使用**文档模型**for Excel 和使用数据挖掘客户端中提供向导**Detailed**报告的选项。 有关详细信息，请参阅[记录挖掘模型&#40;数据挖掘的 Excel 外接程序&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)。  
  
6.  （可选） 单击**参数**可更改算法参数以及自定义挖掘模型的行为。  
  
     “算法参数”对话框包括您在此向导中设置的所有参数，以及一些不常用到的参数，例如 MAXIMUM_SUPPORT。 有关如何使用这些参数的信息，请参阅[Microsoft 关联算法技术参考](data-mining/microsoft-association-algorithm-technical-reference.md)。  
  
7.  上**完成**页上，键入数据集和模型的唯一名称。  
  
8.  在中**选项**，定义想要使用模型完成后：  
  
    -   **浏览**。  在模型准备就绪后，向导将打开一个窗口，该窗口显示规则、项集以及描述关联的依赖关系网络图。  
  
         有关如何解释关联模型查看器中的数据的详细信息，请参阅[浏览关联规则模型](browsing-an-association-rules-model.md)。  
  
    -   **启用钻取**。 选择此选项可以通过模型访问基础数据。  
  
         例如，在您希望单击特定的项集和查看源数据时，钻取很有用。  
  
    -   **使用临时模型**。 如果不希望在服务器上保存的模型，请选择此选项。 在您关闭 Excel 时，临时模型将被删除。  
  
9. 该向导分析所有可能存在的组合，然后创建一个报表，其中包含项集和规则。  
  
## <a name="more-about-association-models"></a>有关关联模型的详细信息  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联规则算法可检查定型数据以查找同时出现在某个事务中的项。 每个组项构成*项集*。 然后，该算法计算每个项集的出现次数，并计算每个项集在所有事务中的相对重要性。  
  
 该算法将使用项集的此信息来生成可用于预测关联或提出建议的规则。 例如，规则可能为“如果用户购买了作者 1 和作者 2 的书各一本，则该用户可能还将购买一本作者 3 的书”。 会根据关联的程度为每个建议指定一个概率。  
  
### <a name="requirements"></a>要求  
 若要使用关联向导，必须连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。  
  
 源数据必须组织为一个事务表。 源数据必须包括含有事务标识符的一列。 此列标识各组项。 该事务列与另一列（项 ID）必须为一对多关系，项 ID 列存储组中各项的名称或 ID 号。  
  
 从概念上讲，试想购物车的例子可能最易于帮助理解。 如果为购物车分配一个 ID，则购物车 ID 将作为交易（事务）的标识符。 购物车中的每件物品（如土豆或牛奶）都是该交易的组成部分。 关联算法可以跨事务跟踪项，例如，确定土豆和牛奶在任何单一交易中出现的次数。  
  
 源数据必须按事务标识符列排序。  
  
## <a name="see-also"></a>请参阅  
 [创建数据挖掘模型](creating-a-data-mining-model.md)   
 [浏览关联规则模型](browsing-an-association-rules-model.md)   
 [购物篮分析&#40;Excel 表分析工具&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)   
 [依赖关系网络关系图演练&#40;数据挖掘外接程序&#41;](dependency-network-diagram-walkthrough-data-mining-add-ins.md)  
  
  
