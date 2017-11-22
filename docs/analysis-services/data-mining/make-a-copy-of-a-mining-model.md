---
title: "创建挖掘模型的副本 |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], copying
- mining models [Analysis Services], creating
- mining models [Analysis Services], how-to topics
- copying mining models
ms.assetid: 7975bb02-f188-49a0-b7de-5b9b216254ad
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ef19138a03ca98b74cfb53703219f6db15875dec
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="make-a-copy-of-a-mining-model"></a>生成挖掘模型的副本
  在要快速创建基于相同数据的多个挖掘模型时，创建挖掘模型的副本将很有用。 在您复制模型后，可以通过更改参数或添加筛选器，编辑新副本。  
  
 例如，如果你有一个链接到购买表的 Customers 表，则可以创建副本以便针对各个客户人口统计学指标生成单独的挖掘模型，并且对年龄或区域之类的属性进行筛选。  
  
 有关如何将模型内容（如图形表示形式或模型模式）复制到剪贴板以供其他程序使用的信息，请参阅 [复制挖掘模型的视图](../../analysis-services/data-mining/copy-a-view-of-a-mining-model.md)。  
  
### <a name="to-create-a-related-mining-model"></a>创建相关的挖掘模型  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的解决方案资源管理器中，单击包含挖掘模型的挖掘结构。  
  
2.  单击 **“挖掘模型”** 选项卡。  
  
3.  选择模型，然后右键单击打开快捷菜单。  
  
     - 或 -  
  
     选择该模型。 在 **“挖掘模型”** 菜单中，选择 **“新建挖掘模型”**。  
  
4.  为新的挖掘模型键入名称，并选择一种算法。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-the-filter-on-the-copied-mining-model"></a>编辑已复制的挖掘模型的筛选器  
  
1.  选择挖掘模型。  
  
2.  在“属性”窗口中，单击“筛选器”属性文本框，再单击 **(...)** 生成按钮。  
  
3.  更改筛选条件。  
  
     有关如何使用筛选器编辑器对话框的详细信息，请参阅[对挖掘模型应用筛选器](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md)。  
  
4.  如果需要，在“属性”窗口的“AlgorithmParameters”文本框中，单击“设置算法参数”，然后根据需要更改算法参数。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型的筛选器（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [从挖掘模型中删除筛选器](../../analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)  
  
  
