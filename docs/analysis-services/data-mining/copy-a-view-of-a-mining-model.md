---
title: 复制挖掘模型的视图 |Microsoft 文档
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 685d4ce90312e9f34dcf9b8a6e0c94b419f37ee4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34014234"
---
# <a name="copy-a-view-of-a-mining-model"></a>复制挖掘模型的视图
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  对于每种类型的挖掘模型， **中数据挖掘设计器的** “挖掘模型查看器” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 选项卡使用单独的查看器。 其中有数种查看器包含可以从中将内容复制到剪贴板的组件，并包含可以从中将内容粘贴到文档或图像处理软件的组件。 下列组件提供了这项功能：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分类查看器和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 序列分类查看器中的分类关系图  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 树查看器和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序查看器中的决策树  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 序列分类查看器中的状态转换  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联规则查看器、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 查看器以及 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 树查看器中的相关性网络  
  
-   从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般内容树查看器的“节点详细信息”窗格中挖掘模型内容  
  
 可以复制整个挖掘模型或仅复制查看器中的可见部分。  
  
> [!WARNING]  
>  使用查看器复制模型时，它不创建新的模型对象。 若要创建新模型，必须使用向导或数据挖掘设计器。 有关详细信息，请参阅 [生成挖掘模型的副本](../../analysis-services/data-mining/make-a-copy-of-a-mining-model.md)。  
  
### <a name="to-copy-the-complete-model-to-the-clipboard"></a>将整个模型复制到剪贴板  
  
1.  从 **“挖掘模型查看器”** 选项卡上的 **“挖掘模型”** 列表中，选择要查看的挖掘模型。  
  
2.  选择适当的选项卡（例如， **“相关性网络”** 选项卡），然后在该选项卡的工具栏上单击 **“复制整个图形”** 。  
  
### <a name="to-copy-the-visible-piece-of-the-model-to-the-clipboard"></a>将模型的可见部分复制到剪贴板  
  
1.  从 **“挖掘模型查看器”** 选项卡上的 **“挖掘模型”** 列表中，选择要查看的挖掘模型。  
  
2.  选择适当的选项卡（例如， **“相关性网络”** 选项卡），然后执行放大或缩小操作以在您想要的级别上查看模型。  
  
3.  在所选选项卡的工具栏上单击 **“复制图形视图”** 。  
  
### <a name="to-copy-the-mining-model-content-to-the-clipboard"></a>将挖掘模型内容复制到剪贴板  
  
1.  从 **“挖掘模型查看器”** 选项卡上的 **“挖掘模型”** 列表中，选择要查看的挖掘模型。  
  
2.  从“查看器”下拉列表中，选择“Microsoft 一般内容树查看器”。  
  
3.  在“节点标题(唯一 ID)”窗格中，单击一个节点。  
  
4.  右键单击“节点详细信息”窗格，然后选择“全选”。  
  
5.  右键再次单击“节点详细信息”窗格，然后选择“复制”。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型查看器任务和操作指南](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
