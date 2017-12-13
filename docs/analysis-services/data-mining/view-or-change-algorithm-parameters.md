---
title: "查看或更改算法参数 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- algorithms [data mining]
- mining models [Analysis Services], algorithms
ms.assetid: 151b899b-c27a-4a09-bcf5-5c9f0ec24168
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9f547511bc918c4b55693207aaf1181da7378c43
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="view-or-change-algorithm-parameters"></a>查看或更改算法参数
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]你可以更改随用于生成数据挖掘模型，以自定义模型的结果的算法一起提供的参数。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中提供的算法参数不仅仅更改模型的属性，它们可用于从根本上更改处理、分组和显示数据的方式。 例如，您可以使用算法参数执行下列操作：  
  
-   更改分析方法，如聚类分析方法。  
  
-   控制功能选择行为。  
  
-   指定项集的大小或规则的概率。  
  
-   控制决策树的分支和深度。  
  
-   指定种子值或用于模型创建的内部维持集的大小。  
  
 为每个算法提供的参数变动很大；有关可以为每个算法设置的参数列表，请参阅本节中的技术参考主题：[数据挖掘算法（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。  
  
### <a name="change-an-algorithm-parameter"></a>更改算法参数  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的数据挖掘设计器的“挖掘模型”选项卡中，右键单击要为其优化算法的挖掘模型的算法类型，选择“设置算法参数”。  
  
     此时将打开 **“算法参数”** 对话框。  
  
2.  在 **“值”** 列中，为要更改的算法设置新值。  
  
     如果未在 **“值”** 列中输入值， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用默认参数值。 **“范围”** 列说明了您可以输入的可能值。  
  
3.  单击 **“确定”**。  
  
     此时，算法参数被设置为新值。 重新处理挖掘模型后，参数更改才反映在该模型中。  
  
### <a name="view-the-parameters-used-in-an-existing-model"></a>查看现有模型中使用的参数  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开一个 DMX 查询窗口。  
  
2.  按如下所示键入查询：  
  
    ```  
    select MINING_PARAMETERS   
    from $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = '<model name>'  
  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
