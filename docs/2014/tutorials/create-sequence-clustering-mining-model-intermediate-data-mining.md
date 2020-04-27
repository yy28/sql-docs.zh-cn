---
title: 创建顺序分析和聚类分析挖掘模型结构（数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e9339227-6c2e-4c4b-8be2-8c1960bc4a8d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b7f4f543952fd86cf6c3c66f9f4b2c51019b1869
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63273481"
---
# <a name="creating-a-sequence-clustering-mining-model-structure-intermediate-data-mining-tutorial"></a>创建顺序分析和聚类分析挖掘模型结构（数据挖掘中级教程）
  要创建顺序分析和聚类分析挖掘模型，第一步是使用数据挖掘向导创建基于 [!INCLUDE[msCoName](../includes/msconame-md.md)] 顺序分析和聚类分析算法的新挖掘结构和挖掘模型。  
  
 您将使用与市场篮分析相同的数据源视图，但需要添加一个包含 `sequence` 标识符的列。 在这种情况下，顺序表示客户将项添加到购物篮中的顺序。  
  
 还要添加一些列，在其中某一模型中使用，用于按照人口统计信息对客户进行分组。  
  
### <a name="to-create-a-sequence-clustering-structure-and-model"></a>创建顺序分析和聚类分析结构和模型  
  
1.  在的解决方案资源管理器[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，右键单击 "**挖掘结构**"，然后选择 "**新建挖掘结构**"。  
  
2.  在 **“欢迎使用数据挖掘向导”** 页上，单击 **“下一步”**。  
  
3.  在 "**选择定义方法**" 页上，验证是否选择了 "**从现有关系数据库或数据仓库**"，然后单击 "**下一步**"。  
  
4.  在 "**创建数据挖掘结构**" 页上，验证是否选择了 "**创建具有挖掘模型的挖掘结构**" 选项。 接下来，单击选项的下拉列表 "**要使用何种数据挖掘技术？**"，然后选择 " **Microsoft 顺序分析**"。 单击“下一步”  。  
  
     此时将显示 "**选择数据源视图**" 页。 在 "**可用数据源视图**" `Orders`下，选择。  
  
     “订单”也是用于市场篮方案的同一数据源视图。 如果尚未创建此数据源视图，请参阅[添加具有嵌套表的数据源视图 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)。  
  
5.  单击“下一步”  。  
  
6.  在 "**指定表类型**" 页上，选中**vAssocSeqOrders**表旁边的 "**事例**" 复选框，然后选中 " **vAssocSeqLineItems** " 表旁边的 "**嵌套**" 复选框。 单击“下一步”  。  
  
    > [!NOTE]  
    >  如果在选择**事例**或**嵌套**复选框时出现错误，则可能是数据源视图中的联接不正确。 嵌套表**vAssocSeqLineItems**必须通过多对一联接连接到事例表， **vAssocSeqOrders** 。 可以通过右键单击联接行并反转联接的方向来编辑关系。 有关详细信息，请参阅 "[创建或编辑关系" 对话框 &#40;Analysis Services 多维数据&#41;](../../2014/analysis-services/create-or-edit-relationship-dialog-box-analysis-services-multidimensional-data.md)。  
  
7.  在 "**指定定型数据**" 页上，通过选中复选框来选择要在模型中使用的列，如下所示：  
  
    -   **IncomeGroup**选中 "**输入**" 复选框。  
  
         此列包含关于客户的重要相关信息，这些信息可以用于聚类分析。 您将在第一个模型中使用这些信息，然后在第二个模型中将其忽略。  
  
    -   **OrderNumber**选中该`Key`复选框。  
  
         此字段将用作事例表的标识符，也就是 `Key`。 一般来说，在任何时候都不应使用事例表的键字段作为输入，因为该键包含的唯一值对聚类分析无用。  
  
    -   **区域**选中 "**输入**" 复选框。  
  
         此列包含关于客户的重要相关信息，这些信息可以用于聚类分析。 您将在第一个模型中使用这些信息，然后在第二个模型中将其忽略。  
  
    -   **LineNumber**选中`Key`和**输入**复选框。  
  
         **LineNumber**字段将用作嵌套表的标识符，或`Sequence Key`。 必须始终将嵌套表的键用于输入。  
  
    -   **模型**选中 "**输入**" 和 "**可预测**" 复选框。  
  
     确认所做选择正确无误，然后单击 "**下一步**"。  
  
8.  在 "**指定列的内容和数据类型"** 页上，验证网格中是否包含下表中显示的列、内容类型和数据类型，然后单击 "**下一步**"。  
  
    |表/列|内容类型|数据类型|  
    |---------------------|------------------|---------------|  
    |IncomeGroup|离散|Text|  
    |OrderNumber|键|Text|  
    |区域|离散|Text|  
    |vAssocSeqLineItems|||  
    |Line Number|键序列|Long|  
    |型号|离散|Text|  
  
9. 在 "**创建测试集**" 页上，将**测试的数据百分比**更改为20，然后单击 "**下一步**"。  
  
10. 在 "**完成向导**" 页的 "**挖掘结构名称**" 中， `Sequence Clustering with Region`键入。  
  
11. 对于 "**挖掘模型名称**"， `Sequence Clustering with Region`请键入。  
  
12. 选中 "**允许钻取**" 框，然后单击 "**完成**"。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [处理顺序分析和聚类分析模型](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘设计器](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 顺序分析和聚类分析算法](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)  
  
  
