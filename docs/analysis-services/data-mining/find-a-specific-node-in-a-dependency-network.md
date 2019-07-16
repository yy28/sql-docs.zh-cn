---
title: 查找特定节点中的依赖关系网络 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ad00f715533e5da24cbec9c61dc79a045fa035ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68183250"
---
# <a name="find-a-specific-node-in-a-dependency-network"></a>在依赖关系网络中查找特定节点
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 挖掘模型中的依赖关系网络可包含许多节点，因此很难找到您感兴趣的数据。 若要解决此问题，请使用数据挖掘设计器的 **“依赖关系网络”** 选项卡上的 **“查找节点”** 对话框来搜索特定节点。  
  
### <a name="to-find-a-specific-node-in-a-dependency-network"></a>在依赖关系网络中查找特定节点  
  
1.  在 **中的** “数据挖掘设计器” **的** “挖掘模型查看器” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡中，单击挖掘模型查看器的 **“依赖关系网络”** 选项卡的工具栏上的 **“查找节点”** 。  
  
     此时，将打开 **“查找节点”** 对话框。  
  
2.  在 **“节点名包含”** 框中，输入您要搜索的节点的名称的一部分。  
  
     此时将筛选节点列表，只显示那些包含部分搜索路径的节点。  
  
3.  从列表中选择正确的节点，然后单击 **“确定”** 。  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型查看器任务和操作指南](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
