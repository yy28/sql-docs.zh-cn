---
title: 向现有挖掘结构中添加挖掘模型 |Microsoft 文档
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e0080ab860b32d9bc7a23eafd54ad14d03db70f2
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
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
  
  
