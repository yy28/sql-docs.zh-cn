---
title: 创建挖掘模型的副本 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7c5479a43a07a6398ff45635828a2a9c88b7cb11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62679462"
---
# <a name="make-a-copy-of-a-mining-model"></a>生成挖掘模型的副本
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在要快速创建基于相同数据的多个挖掘模型时，创建挖掘模型的副本将很有用。 在您复制模型后，可以通过更改参数或添加筛选器，编辑新副本。  
  
 例如，如果你有一个链接到购买表的 Customers 表，则可以创建副本以便针对各个客户人口统计学指标生成单独的挖掘模型，并且对年龄或区域之类的属性进行筛选。  
  
 有关如何将模型内容（如图形表示形式或模型模式）复制到剪贴板以供其他程序使用的信息，请参阅 [复制挖掘模型的视图](../../analysis-services/data-mining/copy-a-view-of-a-mining-model.md)。  
  
### <a name="to-create-a-related-mining-model"></a>创建相关的挖掘模型  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的解决方案资源管理器中，单击包含挖掘模型的挖掘结构。  
  
2.  单击 **“挖掘模型”** 选项卡。  
  
3.  选择模型，然后右键单击打开快捷菜单。  
  
     -或-  
  
     选择该模型。 在 **“挖掘模型”** 菜单中，选择 **“新建挖掘模型”**。  
  
4.  为新的挖掘模型键入名称，并选择一种算法。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-the-filter-on-the-copied-mining-model"></a>编辑已复制的挖掘模型的筛选器  
  
1.  选择挖掘模型。  
  
2.  在中**属性**窗口中，单击文本框**筛选器**属性，然后单击生成 **（...）** 按钮。  
  
3.  更改筛选条件。  
  
     有关如何使用筛选器编辑器对话框的详细信息，请参阅[对挖掘模型应用筛选器](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md)。  
  
4.  如果需要，在“属性”窗口的“AlgorithmParameters”文本框中，单击“设置算法参数”，然后根据需要更改算法参数。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型的筛选器（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [从挖掘模型中删除筛选器](../../analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)  
  
  
