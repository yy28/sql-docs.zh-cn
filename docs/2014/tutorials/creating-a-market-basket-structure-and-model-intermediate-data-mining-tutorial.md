---
title: 创建市场篮结构和模型（数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 659b7a4e-f687-44d9-a60a-86490ccbf90f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 207d82f740b7b5ff174e220e647d67d5bac7f9ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63190824"
---
# <a name="creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial"></a>创建市场篮结构和模型（数据挖掘中级教程）
  您已创建了一个数据源视图，现在将使用数据挖掘向导创建一个新的挖掘结构。 在本任务中，将创建基于 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联算法的挖掘结构和挖掘模型。  
  
> [!NOTE]  
>  如果遇到说明 vAssocSeqLineItems 不能用作嵌套表的错误，请返回本课中的前一个任务，并确保通过从 vAssocSeqLineItems 表（多端）拖到 vAssocSeqOrders 表（一端）来创建多对一联接。 还可以通过右键单击联接线来编辑这两个表之间的关系。  
  
### <a name="to-create-an-association-mining-structure"></a>创建关联挖掘结构  
  
1.  在的解决方案资源管理器[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，右键单击 "**挖掘结构**"，然后选择 "**新建挖掘结构**" 以打开数据挖掘向导。  
  
2.  在 **“欢迎使用数据挖掘向导”** 页上，单击 **“下一步”**。  
  
3.  在 "**选择定义方法**" 页上，验证是否选择了 "**从现有关系数据库或数据仓库**"，然后单击 "**下一步**"。  
  
4.  在 "**创建数据挖掘结构**" 页上，在 "**要使用何种数据挖掘技术？**" 下，从列表中选择 " **Microsoft 关联规则**"，然后单击 "**下一步**"。 此时将显示 "**选择数据源视图**" 页。  
  
5.  选择 "**可用数据源视图**" 下的**订单**，然后单击 "**下一步**"。  
  
6.  在 "**指定表类型**" 页上，在 vAssocSeqLineItems 表的行中选中 "**嵌套**" 复选框，并在嵌套表 vAssocSeqOrders 的行中选中 "**事例**" 复选框。 单击 **下一步**。  
  
7.  在 "**指定定型数据**" 页上，清除可能选中的任何框。 通过选中 "OrderNumber" 旁边的 "**键**" 复选框，为事例表 vAssocSeqOrders 设置密钥。  
  
     由于市场篮分析的目的是确定单个交易中包含哪些产品，因此不必使用**CustomerKey**字段。  
  
8.  通过选择 "模型" 旁边的 "**键**" 复选框，设置嵌套表 vAssocSeqLineItems 的键。 执行此操作时，还会自动选择 "**输入**" 复选框。 同时选中 "**可预测**" `Model`复选框。  
  
     在市场篮模型中，你不关心购物篮中产品的顺序，因此，不应将**LineNumber**作为嵌套表的键。 只在序列非常重要的模型中使用**LineNumber**作为键。 您将在第 4 课中创建使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 顺序分析和聚类分析算法的模型。  
  
9. 选中 IncomeGroup 和 Region 左侧的复选框，但是不进行任何其他选择。 选中最左侧的列会将这些列添加到结构中以供日后参考，但不会用在模型中。 您选择的内容应如下所示：  
  
     ![对话框外观如何](../../2014/tutorials/media/tutorial-configassocmodel.gif "对话框外观如何")  
  
10. 单击 **下一步**。  
  
11. 在 "**指定列的内容和数据类型"** 页上，查看应如下表所示的选择，然后单击 "**下一步**"。  
  
    |列|内容类型|数据类型|  
    |-------------|------------------|---------------|  
    |IncomeGroup|离散|Text|  
    |订单编号|键|Text|  
    |区域|离散|Text|  
    |vAssocSeqLineItems|||  
    |“模型”|键|Text|  
  
12. 在 "**创建测试集**" 页上，"**测试数据百分比**" 选项的默认值为30%。 将此更改为**0**。 单击 **下一步**。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 为测量模型精确度提供不同的图表。 但是，某些精确度图表类型（如提升图和交叉验证报告）旨在进行分类和估计。 关联预测不支持这些方法。  
  
13. 在 "**完成向导**" 页上的 "**挖掘结构名称**" `Association`中，键入。  
  
14. 在 "**挖掘模型名称**" `Association`中，键入。  
  
15. 选择 "**允许钻取**" 选项，然后单击 "**完成**"。  
  
     此时将打开数据挖掘设计器`Association` ，显示您刚创建的挖掘结构。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [&#40;中级数据挖掘教程来修改和处理市场篮模型&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 关联算法](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [内容类型（数据挖掘）](../../2014/analysis-services/data-mining/content-types-data-mining.md)  
  
  
