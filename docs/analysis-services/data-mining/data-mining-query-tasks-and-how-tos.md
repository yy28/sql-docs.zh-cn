---
title: "数据挖掘查询任务和操作指南 |Microsoft 文档"
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
- mining models [Analysis Services], how-to topics
ms.assetid: 1bc2a775-6e62-4c66-a53c-201f2ea66295
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 91ae26748640ae6fbcafe12ae1545fadc2adbde6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="data-mining-query-tasks-and-how-tos"></a>数据挖掘查询任务和操作指南
  创建查询的功能对于使用您的数据挖掘模型十分重要。 本节提供一些示例链接，这些示例演示如何通过使用在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中提供的工具创建针对数据挖掘模型的查询。 有关数据挖掘查询的涵义或可创建的不同类型查询的详细信息，请参阅 [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)。  
  
## <a name="creating-queries-with-prediction-query-builder"></a>使用预测查询生成器创建查询  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中均提供预测查询生成器，作为以图形形式对数据挖掘模型生成查询的一种方法。 下面的主题说明如何选择模型、指定数据源、自定义预测和保存输出。  
  
-   [使用预测查询生成器创建预测查询](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [在数据挖掘设计器中创建单独查询](../../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md)  
  
-   [使用预测查询生成器创建预测查询](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [查看和保存预测查询的结果](../../analysis-services/data-mining/view-and-save-the-results-of-a-prediction-query.md)  
  
-   [手动编辑预测查询](../../analysis-services/data-mining/manually-edit-a-prediction-query.md)  
  
-   [将预测函数应用于模型](../../analysis-services/data-mining/apply-prediction-functions-to-a-model.md)  
  
-   [为预测查询选择和映射输入数据](../../analysis-services/data-mining/choose-and-map-input-data-for-a-prediction-query.md)  
  
## <a name="using-other-data-mining-query-tools"></a>使用其他数据挖掘查询工具  
 除了使用预测查询生成器之外，还可以使用 DMX 或 XMLA 将查询直接键入 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中。 您还可以通过编程方式生成预测查询并且将这些查询发送到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器。 下面的主题提供有关如何在预测查询生成器之外创建和使用预测查询的详细信息。  
  
 [通过模板创建单独预测查询](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md)  
 介绍如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的工具来生成并运行预测查询。  
  
 [通过模板创建单独预测查询](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md)  
 介绍如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中提供的模板来向预测查询添加参数。  
  
 [更改数据挖掘查询的超时值](../../analysis-services/data-mining/change-the-time-out-value-for-data-mining-queries.md)  
 介绍如何在服务器上设置可控制数据挖掘查询的相关行为的属性。  
  
 [针对挖掘模型创建内容查询](../../analysis-services/data-mining/create-a-content-query-on-a-mining-model.md)  
 介绍如何通过使用数据挖掘架构行集来创建返回挖掘模型中存储的详细信息的查询。  
  
 [使用 XMLA 创建数据挖掘查询](../../analysis-services/data-mining/create-a-data-mining-query-by-using-xmla.md)  
 介绍如何通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的 XMLA 模板，创建针对挖掘模型内容的查询。  
  
## <a name="see-also"></a>另请参阅  
 [查询和表达式语言参考 (Analysis Services)](http://msdn.microsoft.com/library/9597533d-35f4-4742-9d8c-7af392163527)   
 [数据挖掘存储过程（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md)  
  
  

