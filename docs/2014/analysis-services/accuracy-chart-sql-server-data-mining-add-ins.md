---
title: 准确性图表 （SQL Server 数据挖掘外接程序） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- accuracy chart
- mining models, validating
- mining models, charting
- lift chart
- mining models, testing
- lift [data mining]
ms.assetid: 303973b4-71c0-4cfc-b7bc-92218b52509d
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 16d669001ae0842c91853e28aae587dd5f4ebb51
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124225"
---
# <a name="accuracy-chart-sql-server-data-mining-add-ins"></a>准确性图表（SQL Server 数据挖掘外接程序）
  ![在功能区中数据挖掘准确性图表按钮](media/dmc-accchart.gif "数据挖掘功能区中的准确性图表按钮")  
  
 通过准确性图表，可以将模型应用于新的数据集，然后评估该模型的性能。 此向导创建准确性图表是*提升图*，这是一种经常用于度量数据挖掘模型的准确性的图表类型。 这种类型的准确性图表以图形方式显示以下改善：即在使用指定数据挖掘模型时，准确性为 100％ 的理想预测与随机预测相比之间的改善。 您可以在一个图表中比较多个模型。  
  
## <a name="example"></a>示例  
 假设 Adventure Works Cycles 的市场部要开展一次定向邮寄活动。 从以往的活动中，他们推算应有 10% 的答复率。 在数据库的一个表中，存储了一个包含 10,000 名潜在客户的列表。 按照正常答复率计算，预计将有 1,000 名客户答复。  
  
 但是，由于他们只能承担向 5,000 名客户邮寄广告的费用，因此市场部使用挖掘模型来寻找最有可能答复的 5,000 名目标客户。  
  
 如果该公司随机选择 5,000 名客户，则估计只能收到 500 个积极答复，因为正常情况下只有 10% 的客户答复。 这正是提升图中的随机线所表示的情况。  
  
 但是，如果市场部使用挖掘模型确定邮寄对象，假设该模型完美无缺的话，则公司可以预期实现这样的结果：向模型建议的 1,000 名潜在客户邮寄广告，会收到所有客户的答复，共计 1,000 份答复。 这正是提升图中的理想线所表示的情况。  
  
## <a name="using-the-accuracy-chart-wizard"></a>使用准确性图表向导  
 若要创建准确性图表，必须参考现有数据挖掘结构。 对于基于该数据挖掘结构的多个模型，只要它们的预测对象相同，就可以衡量它们的准确性。  
  
 如果无法确定哪个结构可用，则可浏览服务器。 有关详细信息，请参阅[Excel 中浏览模型&#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)。  
  
#### <a name="to-create-an-accuracy-chart"></a>创建准确性图表  
  
1.  单击**数据挖掘客户端**功能区。  
  
2.  在**准确性和验证**组中，单击**准确性图表**。  
  
3.  在**选择结构或模型**对话框框中，选择你想要评估的模型。 单击“下一步” 。  
  
    > [!NOTE]  
    >  必须选择与要测试的数据最相匹配的模型。  
  
4.  在**指定列预测和预测的值**对话框框中，选择你想要预测的列和一个目标值，如果适用。 单击“下一步” 。  
  
     例如，在上面的示例中，您可以选择用来建立顾客答复模型的列，并将目标值指定为“可能购买”。  
  
    > [!NOTE]  
    >  不能预测连续值。 但是，可通过将值分割为不同的离散范围，来离散化该列。 在创建数据挖掘模型之前，就必须完成此操作。  
  
5.  在**选择源数据**对话框框中，指定将通过模型通过才能创建预测的数据源。  
  
6.  如果你使用的数据，并不存储模型中，在测试数据的外部源**指定关系**对话框中，映射数据挖掘模型中使用新的源数据与列中的列。  
  
     如果列名称类似，向导将自动映射它们。 虽然输入数据中的某些列可能与分析无关，可以忽略，但某些列是数据挖掘模型处理输入所必需的。 这样的列可能包括事务 ID、目标值或用于预测的列。 如果无法映射所需的列，向导将提供一则警告消息。  
  
7.  单击 **“完成”**。  
  
     向导将创建一个包括提升图和基础数据的报表。  
  
### <a name="requirements"></a>要求  
 如果预测的是离散值，则必须选择要预测的目标值。 例如，如果数据是按照答复“Yes: Buy”(1) 和答复“No: Do Not Buy”(2) 进行分类的，则必须将 1 或 2 指定为预测值。 不过，如果要预测某一范围的值，则可以一次只比较两个值。 例如，如果要预测 5 以上的分数，则可能必须重新标记源数据，并创建一个将结果分为两组（一组大于 5、一组小于 5）的新模型。 然后，可以比较这两组的准确性。  
  
## <a name="understanding-accuracy"></a>了解准确性  
 可以创建两种类型的图表，在一种图表中指定可预测列的状态，而在另一种中不指定该状态。  
  
 如果指定可预测列的状态，则该图表的 X 轴表示用于比较预测的测试数据集的百分比。 该图表的 Y 轴表示预测为指定状态的值的百分比。  
  
 如果不指定可预测列的状态，则图表将显示模型针对所有可能预测的准确性。  
  
 有关提升图工作原理以及如何基于随机预测线和理想预测线计算准确性的详细信息，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书中的主题“提升图”。  
  
## <a name="see-also"></a>请参阅  
 [验证模型和使用预测模型&#40;数据挖掘的 Excel 外接程序&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  