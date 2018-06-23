---
title: 第 4 课： 生成序列聚类分析方案 （数据挖掘中级教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- sequence clustering algorithms [Analysis Services]
- tutorials [Data Mining]
ms.assetid: 63436bbd-0f73-4012-b6f1-358c81e4d92a
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7bfa4dd3a739e81b5a7f10cda0b17452fe48c4d0
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36311875"
---
# <a name="lesson-4-building-a-sequence-clustering-scenario-intermediate-data-mining-tutorial"></a>第 4 课：生成顺序分析和聚类分析方案（数据挖掘中级教程）
  市场部[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]想要了解客户浏览[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]Web 站点。 公司认为存在一个顺序模式，客户以这种模式将产品放入其购物篮中。 它们希望分析购买序列的顺序，以了解客户如何向其购物篮中添加相关产品。 然后可使用上述信息简化网站的流程，这样便可引导客户购买更多的产品。  
  
 完成本课程中的任务时，您已经创建了一个挖掘模型，该模型使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 顺序分析和聚类分析算法预测客户将放入购物篮中的下一个产品。 您将试用两个版本的模型：一个模型仅分析购物篮中产品的顺序，另一个模型中包含一些其他可用来进行聚类分析的客户统计信息。 最后，您将使用这些模型创建预测，以向客户推荐产品。  
  
 若要在本课程中完成的任务，将使用你在中创建的市场篮挖掘结构[第 3 课： 生成市场篮方案&#40;数据挖掘中级教程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)。 本课程包含以下任务：  
  
-   [创建序列聚类分析挖掘模型结构&#40;中间数据挖掘教程&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
-   [处理顺序分析和聚类分析模型](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
-   [浏览聚类分析模型的序列&#40;中间数据挖掘教程&#41;](../../2014/tutorials/exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [创建相关的序列聚类分析模型&#40;中间数据挖掘教程&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [在聚类分析模型的序列上创建预测&#40;中间数据挖掘教程&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建序列聚类分析挖掘模型结构&#40;中间数据挖掘教程&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>所有课程  
 [第 1 课： 创建中级数据挖掘解决方案&#40;中间数据挖掘教程&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [第 2 课： 生成预测方案&#40;中间数据挖掘教程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [第 3 课： 生成市场篮方案&#40;中间数据挖掘教程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 第 4 课：顺序分析和聚类分析方案（数据挖掘中级教程）  
  
 [第 5 课： 生成神经网络和逻辑回归模型&#40;中间数据挖掘教程&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘基础教程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [中间数据挖掘教程&#40;Analysis Services-数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  