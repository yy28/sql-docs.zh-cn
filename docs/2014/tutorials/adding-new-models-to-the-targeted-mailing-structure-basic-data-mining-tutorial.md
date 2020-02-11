---
title: 向目标邮件结构添加新模型（数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 512c6888-60f1-46e4-9639-bc448395b8d7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 285ee82110ffdef521d75fb43343f4889663e981
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62822626"
---
# <a name="adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>向 Targeted Mailing 结构中添加新模型（数据挖掘基础教程）
  在此任务中，您将使用数据挖掘设计器的 "**挖掘模型**" 选项卡定义另外两个模型。 您将使用 Microsoft 聚类分析算法和 Microsoft Naive Bayes 算法创建模型。 之所以选择这两种算法，是因为它们能够预测离散值（例如，自行车购买行为）。 有关这些算法的详细信息，请参阅[Microsoft 聚类分析算法](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)和[Microsoft Naive Bayes 算法](../../2014/analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)  
  
### <a name="to-create-a-clustering-mining-model"></a>创建聚类分析挖掘模型  
  
1.  切换到中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]数据挖掘设计器中的 "**挖掘模型**" 选项卡。  
  
     请注意，设计器将显示两个列，一个用于挖掘结构，另`TM_Decision_Tree`一个用于在上一课中创建的挖掘模型。  
  
2.  右键单击 "**结构**" 列，然后选择 "**新建挖掘模型**"。  
  
3.  在 "**新建挖掘模型**" 对话框中的 "**模型名称**" `TM_Clustering`中，键入。  
  
4.  在 "**算法名称**" 中选择 " **Microsoft 群集**"。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 新模型现在会显示在数据挖掘设计器的 "**挖掘模型**" 选项卡中。 此模型是[!INCLUDE[msCoName](../includes/msconame-md.md)]通过聚类分析算法生成的，它将具有类似特征的客户分组到群集中，并为每个分类预测自行车购买量。 虽然您可以修改新模型的列用法和属性，但本教程不需要对`TM_Clustering`模型进行任何更改。  
  
### <a name="to-create-a-naive-bayes-mining-model"></a>创建 Naive Bayes 挖掘模型  
  
1.  在数据挖掘设计器的 "**挖掘模型**" 选项卡中，右键单击 productsportal**结构**列，然后选择 "**新建挖掘模型**"。  
  
2.  在 "**新建挖掘模型**" 对话框中的 "**模型名称**" `TM_NaiveBayes`下，键入。  
  
3.  在 "**算法名称**" 中，选择 " **Microsoft Naive Bayes**"，然后单击 **"确定"**。  
  
     此时会出现一条消息[!INCLUDE[msCoName](../includes/msconame-md.md)] ，指出 Naive Bayes 算法不支持**年龄**列和**每年收入**列，这是连续的。  
  
4.  单击 **"是"** 以确认消息并继续。  
  
 新模型将显示在数据挖掘设计器的 "**挖掘模型**" 选项卡中。 虽然您可以修改此选项卡中所有模型的列用法和属性，但本教程不需要`TM_NaiveBayes`对模型进行任何更改。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [在目标邮件结构中处理模型 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [向结构中添加挖掘模型 &#40;Analysis Services 数据挖掘&#41;](../../2014/analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)   
 [数据挖掘设计器](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [移动数据挖掘对象](../../2014/analysis-services/data-mining/moving-data-mining-objects.md)  
  
  
