---
title: 创建序列聚类分析挖掘模型结构 （数据挖掘中级教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e9339227-6c2e-4c4b-8be2-8c1960bc4a8d
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 09aaac50873d6c4c63b46fdf37dd7ee854000886
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312695"
---
# <a name="creating-a-sequence-clustering-mining-model-structure-intermediate-data-mining-tutorial"></a>创建顺序分析和聚类分析挖掘模型结构（数据挖掘中级教程）
  要创建顺序分析和聚类分析挖掘模型，第一步是使用数据挖掘向导创建基于 [!INCLUDE[msCoName](../includes/msconame-md.md)] 顺序分析和聚类分析算法的新挖掘结构和挖掘模型。  
  
 您将使用与市场篮分析相同的数据源视图，但需要添加一个包含 `sequence` 标识符的列。 在这种情况下，顺序表示客户将项添加到购物篮中的顺序。  
  
 还要添加一些列，在其中某一模型中使用，用于按照人口统计信息对客户进行分组。  
  
### <a name="to-create-a-sequence-clustering-structure-and-model"></a>创建顺序分析和聚类分析结构和模型  
  
1.  在解决方案资源管理器中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，右键单击**挖掘结构**和选择**新挖掘结构**。  
  
2.  在 **“欢迎使用数据挖掘向导”** 页上，单击 **“下一步”**。  
  
3.  上**选择定义方法**页上，确认**从现有关系数据库或数据仓库**已选择，然后单击**下一步**。  
  
4.  上**创建数据挖掘结构**页上，确认选项**创建具有挖掘模型的挖掘结构**选择。 接下来，单击下拉列表选项时，**你想要使用何种数据挖掘技术？**，然后选择**Microsoft Sequence Clustering**。 单击“下一步” 。  
  
     **选择数据源视图**页将出现。 下**可用数据源视图**，选择`Orders`。  
  
     “订单”也是用于市场篮方案的同一数据源视图。 如果你尚未创建此数据源视图，请参阅[添加具有嵌套表的数据源视图&#40;中间 Data Mining Tutorial&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)。  
  
5.  单击“下一步” 。  
  
6.  上**指定表类型**页上，选择**用例**旁边的复选框**vAssocSeqOrders**表，然后选择**嵌套**复选框旁边**vAssocSeqLineItems**表。 单击“下一步” 。  
  
    > [!NOTE]  
    >  如果你选择时发生了错误**用例**或**嵌套**复选框，它可能是数据源视图中的连接不正确。 嵌套的表， **vAssocSeqLineItems**，必须连接到事例表中， **vAssocSeqOrders，** 由多对一联接。 可以通过右键单击联接行并反转联接的方向来编辑关系。 有关详细信息，请参阅[创建或编辑关系对话框&#40;Analysis Services-多维数据&#41;](../../2014/analysis-services/create-or-edit-relationship-dialog-box-analysis-services-multidimensional-data.md)。  
  
7.  上**指定定型数据**页上，在模型中选择使用的列，通过选中一个复选框，如下所示：  
  
    -   **IncomeGroup**选择**输入**复选框。  
  
         此列包含关于客户的重要相关信息，这些信息可以用于聚类分析。 您将在第一个模型中使用这些信息，然后在第二个模型中将其忽略。  
  
    -   **OrderNumber**选择`Key`复选框。  
  
         此字段将用作事例表的标识符，也就是 `Key`。 一般来说，在任何时候都不应使用事例表的键字段作为输入，因为该键包含的唯一值对聚类分析无用。  
  
    -   **区域**选择**输入**复选框。  
  
         此列包含关于客户的重要相关信息，这些信息可以用于聚类分析。 您将在第一个模型中使用这些信息，然后在第二个模型中将其忽略。  
  
    -   **LineNumber**选择`Key`和**输入**复选框。  
  
         **LineNumber**字段将用作标识符对于嵌套表，或`Sequence Key`。 必须始终将嵌套表的键用于输入。  
  
    -   **模型**选择**输入**和**可预测**复选框。  
  
     验证所选内容正确无误，然后单击**下一步**。  
  
8.  上**指定列的内容和数据类型**页上，验证该网格包含列、 内容类型和下表中所示的数据类型，然后单击**下一步**。  
  
    |表/列|内容类型|数据类型|  
    |---------------------|------------------|---------------|  
    |IncomeGroup|离散|文本|  
    |OrderNumber|Key|文本|  
    |地区|离散|文本|  
    |vAssocSeqLineItems|||  
    |Line Number|键序列|Long|  
    |“模型”|离散|文本|  
  
9. 上**创建测试集**页上，更改**的数据以供测试百分比**为 20，然后单击**下一步**。  
  
10. 上**完成向导**页上，为**挖掘结构名称**，类型`Sequence Clustering with Region`。  
  
11. 有关**挖掘模型名称**，类型`Sequence Clustering with Region`。  
  
12. 检查**允许钻取**框中，并依次**完成**。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [处理顺序分析和聚类分析模型](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘设计器](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 顺序分析和聚类分析算法](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)  
  
  