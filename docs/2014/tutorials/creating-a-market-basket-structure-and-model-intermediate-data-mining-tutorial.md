---
title: 创建市场篮结构和模型 （数据挖掘中级教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 659b7a4e-f687-44d9-a60a-86490ccbf90f
caps.latest.revision: 48
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 957a55114e5a4fb756c63b63779eed3fbfb5f95b
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312595"
---
# <a name="creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial"></a>创建市场篮结构和模型（数据挖掘中级教程）
  您已创建了一个数据源视图，现在将使用数据挖掘向导创建一个新的挖掘结构。 在本任务中，将创建基于 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联算法的挖掘结构和挖掘模型。  
  
> [!NOTE]  
>  如果遇到说明 vAssocSeqLineItems 不能用作嵌套表的错误，请返回本课中的前一个任务，并确保通过从 vAssocSeqLineItems 表（多端）拖到 vAssocSeqOrders 表（一端）来创建多对一联接。 还可以通过右键单击联接线来编辑这两个表之间的关系。  
  
### <a name="to-create-an-association-mining-structure"></a>创建关联挖掘结构  
  
1.  在解决方案资源管理器中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，右键单击**挖掘结构**和选择**新挖掘结构**以打开数据挖掘向导。  
  
2.  在 **“欢迎使用数据挖掘向导”** 页上，单击 **“下一步”**。  
  
3.  上**选择定义方法**页上，确认**从现有关系数据库或数据仓库**已选择，然后单击**下一步**。  
  
4.  上**创建数据挖掘结构**页上，在**你想要使用何种数据挖掘技术？**，选择**Microsoft 关联规则**从列表，然后单击**下一步**。 **选择数据源视图**页将出现。  
  
5.  选择**订单**下**可用数据源视图**，然后单击**下一步**。  
  
6.  上**指定表类型**页上，对于 vAssocSeqLineItems 表中，行中的选择**嵌套**复选框，然后在嵌套的表 vAssocSeqOrders 行中，选择**用例**复选框。 单击“下一步” 。  
  
7.  上**指定定型数据**页上，清除任何可能要检查的框。 设置的密钥，事例表中，vAssocSeqOrders，选择**密钥**OrderNumber 旁边的复选框。  
  
     因为市场篮分析的目的是确定哪些产品包括在单个事务中，你无需使用**CustomerKey**字段。  
  
8.  设置的密钥，嵌套表，vAssocSeqLineItems，选择**密钥**模型旁边的复选框。 **输入**执行此操作时，还会自动选中复选框。 选择**可预测**复选框`Model`以及。  
  
     在市场篮模型中，你不关心的购物篮中的产品序列并因此不应包含**LineNumber**作为嵌套表的键。 你将使用**LineNumber**作为仅中的顺序非常重要的模型的键。 您将在第 4 课中创建使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 顺序分析和聚类分析算法的模型。  
  
9. 选中 IncomeGroup 和 Region 左侧的复选框，但是不进行任何其他选择。 选中最左侧的列会将这些列添加到结构中以供日后参考，但不会用在模型中。 您选择的内容应如下所示：  
  
     ![如何对话框看起来应](../../2014/tutorials/media/tutorial-configassocmodel.gif "对话框应外观")  
  
10. 单击“下一步” 。  
  
11. 上**指定列的内容和数据类型**页上，查看所选择的该值应进行下表中所示，然后单击**下一步**。  
  
    |“列”|内容类型|数据类型|  
    |-------------|------------------|---------------|  
    |IncomeGroup|离散|文本|  
    |Order Number|Key|文本|  
    |地区|离散|文本|  
    |vAssocSeqLineItems|||  
    |“模型”|Key|文本|  
  
12. 上**创建测试设置**页上，该选项的默认值**的数据以供测试百分比**是 30%。 将此更改为**0**。 单击“下一步” 。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 为测量模型精确度提供不同的图表。 但是，某些精确度图表类型（如提升图和交叉验证报告）旨在进行分类和估计。 关联预测不支持这些方法。  
  
13. 上**完成向导**页上，在**挖掘结构名称**，类型`Association`。  
  
14. 在**挖掘模型名称**，类型`Association`。  
  
15. 选择选项**允许钻取**，然后单击**完成**。  
  
     数据挖掘设计器将打开以显示`Association`刚创建的挖掘结构。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [修改和处理市场篮模型&#40;中间数据挖掘教程&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 关联算法](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [内容类型&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)  
  
  