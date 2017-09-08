---
title: "筛选器中关联的规则规则模型 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filtering rules [Analysis Services]
- Mining Model Viewer [Analysis Services], rules
- Rules Viewer
ms.assetid: 26cdba5b-5bf1-439e-80a3-8759774e918b
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 88eb75188ed36a8a79178f6b893c5301ffd2d47e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="filter-a-rule-in-an-association-rules-model"></a>筛选关联规则模型中的规则
  您可以将筛选与关联模型一起使用来限制结果，使其仅包含您感兴趣的关联。 例如，您可以筛选规则，以便仅显示包含特定产品的规则。  
  
 在数据挖掘设计器中，可使用  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联规则查看器的“规则”选项卡上的控件来筛选所显示的规则。  你还可以创建一个基于模型的查询，只查看包含特定值的项集。  
  
> [!NOTE]  
>  此选项仅可用于使用 Microsoft 关联算法创建的挖掘模型。  
  
### <a name="filter-a-rule-in-an-association-model"></a>筛选关联模型中的规则  
  
1.  使用 **“关联规则查看器”**打开挖掘模型。 若要在 SQL Server Management Studio 中执行此操作，右键单击模型名称，然后选择 **“浏览”**。 若要在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中执行此操作，请双击包含该模型的挖掘结构，然后单击“数据挖掘设计器”的“挖掘模型查看器”选项卡。  
  
2.  单击 **“关联规则查看器”** 的 **“规则”**选项卡。  
  
3.  在 **“筛选规则”** 框中键入规则条件。 例如，规则条件可以为“Bike Stand”，该条件还可以返回“Bike Stands”。  
  
     **“筛选规则”** 文本框支持用 .NET 语言定义的正则表达式。 因此，可使用如下所示的表达式： `((.Helmets.*Fenders.*)|(.*Fenders.*Helmets.*))`。 此表达式将返回特定项集，其中包括的属性具有以各种顺序显示的词语“Helmets”和“Fenders”。  
  
4.  对于 **“最小概率”**，增大概率值以查看较少的规则，减小概率值以查看较多的规则。  
  
5.  对于 **“最低重要性”**，增大重要性的值以查看较少的规则，减小该值以查看较多的规则。  
  
6.  对于 **“显示”**，选择以下选项之一： **“显示属性名称和值”**、 **“仅显示属性名称”**或 **“仅显示属性值”**。  
  
7.  对于 **“最大行数”**，增大该值以增加符合指定条件的规则的总数，减小该值以限制返回的规则数。 规则按概率排序，所以您可以消除符合指定的概率或重要性条件的其他规则。  
  
8.  选中或取消选中 **“显示长名称”** 复选框以切换规则名称的显示方式。  
  
     现在筛选过的规则将仅显示包含所指项的那些规则。 筛选条件可应用到属性值中的规则分隔符“->”之前或之后。  
  
    > [!NOTE]  
    >  查看器基于挖掘模型的查询对规则的初始列表进行缓存；除非您通过设置最大行数、概率、重要性或长名称的显示方式来更改查询条件，否则查看器不刷新规则列表。 因此，如果键入了某一条件而显示并未立即刷新，则可以通过先选中再取消选中 **“显示长名称”** 复选框强制查看器刷新数据。  
  
### <a name="create-a-query-on-the-itemsets-in-an-association-model"></a>针对关联模型中的项集创建查询  
  
-   [关联模型查询示例](../../analysis-services/data-mining/association-model-query-examples.md)  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型查看器任务和操作指南](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [使用 Microsoft 关联规则查看器浏览模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)   
 [第 3 课： 生成市场篮方案 &#40; 数据挖掘中级教程 &#41;](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a)  
  
  
