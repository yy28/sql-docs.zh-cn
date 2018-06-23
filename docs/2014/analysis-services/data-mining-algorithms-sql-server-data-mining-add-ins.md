---
title: 数据挖掘算法 （SQL Server 数据挖掘外接程序） |Microsoft 文档
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
- segmentation
- data mining algorithms
- clustering [data mining]
- linear regression
- association [data mining]
- neural networks
- logistic regression
- regression
- sequence analysis
- decision tree [data mining]
- Naive Bayes
- time series [data mining]
ms.assetid: 3a1a62e4-9fb5-4cdb-a6c6-1b8b30d417ef
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4ea33a6ee29965202189fd4149c243df3d1d91df
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128003"
---
# <a name="data-mining-algorithms-sql-server-data-mining-add-ins"></a>数据挖掘算法（SQL Server 数据挖掘外接程序）
  Office 数据挖掘外接程序支持使用以下数据挖掘算法创建分析模型。 所有算法基于已知的计算机学习方法，并已由 Microsoft 研究院实现。  
  
## <a name="algorithms"></a>算法  
  
|计算机学习方法|工作方式|  
|-----------------------------|------------------|  
|Microsoft 关联规则算法|了解哪些产品一起被购买或哪些事件一起发生，并使用该模型生成一些建议。<br /><br /> [http://msdn.microsoft.com/library/ms174916.aspx](http://msdn.microsoft.com/library/ms174916.aspx)|  
|Microsoft 聚类分析算法|定义市场细分，自动将相关客户归入一组，或在数据中查找关系以供进一步挖掘时使用。<br /><br /> [http://msdn.microsoft.com/library/ms174879.aspx](http://msdn.microsoft.com/library/ms174879.aspx)|  
|Microsoft 决策树算法|识别数据的各个元素之间的以前未知的关系，以更好地进行决策或查找导致特定结果的因素。<br /><br /> [http://msdn.microsoft.com/library/ms174923.aspx](http://msdn.microsoft.com/library/ms174923.aspx)|  
|Microsoft 线性回归算法|查找描述导致数值结果的因素的数学表达式。<br /><br /> [http://msdn.microsoft.com/library/ms174824.aspx](http://msdn.microsoft.com/library/ms174824.aspx)|  
|Microsoft 逻辑回归算法|识别导致二进制结果的因素，并了解如何使用它们来影响结果。<br /><br /> [http://msdn.microsoft.com/library/ms174828.aspx](http://msdn.microsoft.com/library/ms174828.aspx)|  
|Microsoft Naïve Bayes 算法|发现数据中的关系并查找那些与结果最有关的关系。<br /><br /> [http://msdn.microsoft.com/en-us/library/ms174806.aspx](http://msdn.microsoft.com/library/ms174806.aspx)|  
|Microsoft 神经网络算法|查找多个输入以及甚至多个输出之间隐藏的关系。 用于探索或预测。<br /><br /> [http://msdn.microsoft.com/library/ms174941.aspx](http://msdn.microsoft.com/library/ms174941.aspx)|  
|Microsoft 时序算法|使用历史数据来预测将来的值。<br /><br /> [http://msdn.microsoft.com/library/ms174923.aspx](http://msdn.microsoft.com/library/ms174923.aspx)|  
  
## <a name="advanced-options"></a>“高级选项”  
 使用 Excel 数据挖掘客户端时，您可以选择创建自己的数据挖掘结构和模型，或优化算法的参数。  
  
 [算法参数&#40;SQL Server 数据挖掘外接程序&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md)  
  
 使用这些高级选项可以两种方式来自定义您的模型：  
  
-   使用 **“数据挖掘查询”** 向导创建您的模型。  
  
-   在 **“数据挖掘客户端”** 中，在启动向导后，单击 **“参数”**。  
  
## <a name="see-also"></a>请参阅  
 [查询&#40;SQL Server 数据挖掘外接程序&#41;](query-sql-server-data-mining-add-ins.md)   
 [高级建模&#40;数据挖掘的 Excel 外接程序&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)  
  
  