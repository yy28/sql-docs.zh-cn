---
title: "创建交叉验证报表 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- validating data mining models
- mining structures [Analysis Services], how-to topics
- cross-validation [data mining]
- statistical standard deviation
ms.assetid: 7b1fec4c-7053-41eb-b030-5179257967a4
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 87f3809146240a6e807cad3a5e1e22981f8bbf4d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-cross-validation-report"></a>创建交叉验证报表
  本主题演练如何在数据挖掘设计器中使用“准确性图表”选项卡创建交叉验证报表。 有关交叉验证报表外观的常规信息，以及该报表包含的统计度量值，请参阅[交叉验证（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)。  
  
 交叉验证报表在本质上不同于提升图或分类矩阵之类的准确性图表。  
  
-   交叉验证评估在模型或结构中使用的数据的总体分布情况；因此，您不指定测试数据集。 交叉验证始终仅使用用于对模型或挖掘结构进行定型的原始数据。  
  
-   只能针对单个可预测结果执行交叉验证。 如果结构支持具有不同可预测属性的模型，则您必须为每个可预测输出都创建单独的报表。  
  
-   只有与当前所选结构相关的模型才可用于交叉验证。  
  
-   如果当前选择的结构支持聚类分析模型和非聚类分析模型的组合，则在你单击“获取结果”时，交叉验证存储过程将自动加载具有相同预测列的模型，并且忽略不共享相同可预测属性的聚类分析模型。  
  
-   只有在挖掘模型不支持任何其他可预测属性的情况下，您才可以对不具有可预测属性的聚类分析模型创建交叉验证报表。  
  
### <a name="select-a-mining-structure"></a>选择挖掘结构  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开数据挖掘设计器。  
  
2.  在解决方案资源管理器中，打开包含要为其创建报表的结构或模型的数据库。  
  
3.  在数据挖掘设计器中，双击挖掘结构以打开结构及其相关模型。  
  
4.  单击 **“挖掘准确性图表”** 选项卡。  
  
5.  单击 **“交叉验证”** 选项卡。  
  
### <a name="set-cross-validation-options"></a>设置交叉验证选项  
  
1.  在 **“交叉验证”** 选项卡中，对于 **“折叠计数”**，单击向下箭头，选择一个 1 到 10 之间的数字。 默认值为 10。  
  
     **“折叠计数”** 表示将在原始数据集中创建的分区数。 如果将“折叠计数”设置为 1，则将在不分区的情况下使用定型集。  
  
2.  对于 **“目标属性”**，单击向下箭头，从列表中选择一个列。 如果模型是聚类分析模型，则选择 **#Cluster** ，以指示该模型不具有可预测属性。 请注意，只有在挖掘结构不支持其他类型的可预测属性的情况下，值 **#Cluster**才可用。  
  
     只能为每个报表选择一个可预测属性。 默认情况下，所有具有同一可预测属性的相关模型都包括在一个报表中。  
  
3.  对于 **“最大事例数”**，键入一个足够大的数字，以便在将数据拆分到指定的折叠数中时提供数据的典型事例。 如果数字大于模型定型集中的事例计数，将使用所有的事例。  
  
     如果定型数据集很大，则对 **“最大事例数”** 的值进行设置将会限制已处理事例的总数，从而加快报表完成的速度。 但是，不应将“最大事例数”设置得过低，否则将没有足够的数据可用于交叉验证。  
  
4.  或者，对于 **“目标状态”**，键入希望建模的可预测属性的值。 例如，如果 [Bike Buyer] 列有两个可能的值：1 (Yes) 和 2 (No)，则可以输入值 1 来仅为预期结果评估模型的准确性。  
  
    > [!NOTE]  
    >  如果未输入值，“目标阈值”选项将不可用，并且将会针对可预测属性的所有可能的值对该模型进行评估。  
  
5.  或者，对于 **“目标阈值”**，键入一个 0 到 1 之间的十进制数字，来指定预测一定会计为准确的最小概率。  
  
     有关如何设置概率阈值的更多技巧，请参阅 [交叉验证报表中的度量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。  
  
6.  单击 **“获取结果”**。  
  
### <a name="print-the-cross-validation-report"></a>打印交叉验证报表  
  
1.  在“交叉验证”选项卡中，右键单击已完成的报表。  
  
2.  在快捷菜单中，选择 **“打印”** 或 **“打印预览”** 来预先查看该报表。  
  
### <a name="create-a-copy-of-the-report-in-microsoft-excel"></a>在 Microsoft Excel 中创建报表的副本  
  
1.  在“交叉验证”选项卡中，右键单击已完成的报表。  
  
2.  在快捷菜单中，选择 **“全选”**。  
  
3.  右键单击所选文本，然后选择“复制”。  
  
4.  将所选内容粘贴到一个打开的 Excel 工作簿中。 如果使用的是 **“粘贴”** 选项，该报表将作为 HTML 粘贴到 Excel 中，其中保留了行和列的格式。 如果使用的是用于文本或 Unicode 文本的“选择性粘贴”选项粘贴报表，将以行分隔的格式粘贴报表。  
  
## <a name="see-also"></a>另请参阅  
 [交叉验证报表中的度量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)  
  
  

