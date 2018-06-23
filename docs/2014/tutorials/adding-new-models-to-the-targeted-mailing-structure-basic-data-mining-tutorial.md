---
title: 将新模型添加到目标的邮件结构 （数据挖掘基础教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 512c6888-60f1-46e4-9639-bc448395b8d7
caps.latest.revision: 45
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c5e31e06a489b1807335f63dd1675fc9e77c45b4
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312375"
---
# <a name="adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>向 Targeted Mailing 结构中添加新模型（数据挖掘基础教程）
  在此任务中，你将使用定义两个其他模型**挖掘模型**数据挖掘设计器选项卡。 您将使用 Microsoft 聚类分析算法和 Microsoft Naive Bayes 算法创建模型。 之所以选择这两种算法，是因为它们能够预测离散值（例如，自行车购买行为）。 有关这些算法的详细信息，请参阅[Microsoft 聚类分析算法](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)和[Microsoft Naive Bayes 算法](../../2014/analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)  
  
### <a name="to-create-a-clustering-mining-model"></a>创建聚类分析挖掘模型  
  
1.  切换到**挖掘模型**数据挖掘设计器中的选项卡[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
     请注意，设计器会显示两个列，一个挖掘结构，一个用于`TM_Decision_Tree`你在上一课中创建的挖掘模型。  
  
2.  右键单击**结构**列并选择**新建挖掘模型**。  
  
3.  在**新建挖掘模型**对话框中，在**模型名称**，类型`TM_Clustering`。  
  
4.  在**算法名称**，选择**Microsoft 聚类分析**。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 新模型现在将显示在**挖掘模型**数据挖掘设计器选项卡。 此模型中，用生成[!INCLUDE[msCoName](../includes/msconame-md.md)]聚类分析算法，分组具有类似特征到群集的客户，并预测自行车购买为每个群集。 虽然您可以修改的列使用情况和属性的新模型，无变化`TM_Clustering`模型所需的本教程。  
  
### <a name="to-create-a-naive-bayes-mining-model"></a>创建 Naive Bayes 挖掘模型  
  
1.  在**挖掘模型**选项卡上的数据挖掘设计器中，右键单击**结构**列，并选择**新建挖掘模型**。  
  
2.  在**新建挖掘模型**对话框中，在**模型名称**，类型`TM_NaiveBayes`。  
  
3.  在**算法名称**，选择**Microsoft Naive Bayes**，然后单击**确定**。  
  
     显示一条消息，指出[!INCLUDE[msCoName](../includes/msconame-md.md)]Naive Bayes 算法不支持**年龄**和**Yearly Income**是连续的列。  
  
4.  单击**是**确认消息并继续。  
  
 新模型将显示在**挖掘模型**数据挖掘设计器选项卡。 虽然您可以修改的列使用情况和中的所有模型的属性选项卡，对做任何更改`TM_NaiveBayes`模型所需的本教程。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [处理目标的邮件结构中的模型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [向结构中添加挖掘模型&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)   
 [数据挖掘设计器](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [移动数据挖掘对象](../../2014/analysis-services/data-mining/moving-data-mining-objects.md)  
  
  