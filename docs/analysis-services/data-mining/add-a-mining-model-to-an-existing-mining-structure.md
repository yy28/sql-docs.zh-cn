---
title: "向现有挖掘结构中添加挖掘模型 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], adding
- mining structures [Analysis Services], mining models
- adding mining models
ms.assetid: fcf72300-0674-4e73-a826-9b8eeffefbb5
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ecd909a6aeb0fb0b7d0557ba93333709f5ade242
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="add-a-mining-model-to-an-existing-mining-structure"></a>在现有挖掘结构中添加挖掘模型
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
在添加初始模型后，可以将更多挖掘模型添加到挖掘结构中。 每个模型必须包含在结构中存在的列，但您可以为每个挖掘模型定义不同的列用法。 有关如何定义挖掘模型列的详细信息，请参阅 [挖掘模型列](../../analysis-services/data-mining/mining-model-columns.md)。  
  
### <a name="to-add-a-mining-model-to-the-structure"></a>在结构中添加挖掘模型  
  
1.  在 **中的** “挖掘模型” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]菜单项中，选择 **“新建挖掘模型”**。  
  
     此时将打开 **“新建挖掘模型”** 对话框。  
  
2.  在 **“模型名称”**下面，输入新挖掘模型的名称。  
  
3.  在 **“算法名称”**下面，选择将用来生成挖掘模型的算法。  
  
4.  单击 **“确定”**。  
  
 新模型将显示在 **“挖掘模型”** 选项卡中。模型使用结构中存在的默认列。 有关如何修改列的信息，请参阅 [更改挖掘模型的属性](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
