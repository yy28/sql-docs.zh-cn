---
title: 筛选项集在关联规则模型 |Microsoft 文档
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
- itemsets [Analysis Services]
- filtering itemsets [Analysis Services]
- Mining Model Viewer [Analysis Services], itemsets
ms.assetid: 3ed919ea-8598-45d2-a4a0-b1b3357a4ab1
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c7bee45242d761b87d4cae3c112fe67a3b17509e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024449"
---
# <a name="filter-an-itemset-in-an-association-rules-model"></a>在关联规则模型中筛选项集
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，可以筛选 **关联规则查看器的** “项集” [!INCLUDE[msCoName](../../includes/msconame-md.md)] 选项卡中显示的项集。  
  
### <a name="to-filter-an-itemset"></a>筛选项集  
  
1.  在 **中的数据挖掘设计器的** “挖掘模型查看器” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡上，单击 **“关联规则查看器”** 的 **“项集”** 选项卡。  
  
2.  在 **“筛选项集”** 框中输入规则条件。 例如，规则条件可以为“Touring-1000 = existing”  
  
3.  单击 **“输入”**。  
  
 现在便对项集进行了筛选以仅显示包含所选项的那些项集。 该框不区分大小写。 筛选器存储在内存中，因此您可以从列表中选择过去使用的筛选器。  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型查看器任务和操作指南](mining-model-viewer-tasks-and-how-tos.md)  
  
  