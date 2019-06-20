---
title: 查看时序公式模型 （数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- ARTXP
- time series algorithms [Analysis Services]
- ARIMA
- time series [Analysis Services]
- Time Series Viewer [Analysis Services]
ms.assetid: 825ef719-2f44-4979-be01-5a81f54e1a53
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 43382b5dd8a20de1454bfc3d6a16aa68c99e34a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082601"
---
# <a name="view-the-formula-for-a-time-series-model-data-mining"></a>查看时序模型的公式（数据挖掘）
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]时序查看器 inData 挖掘设计器提供的最简单的方式查看时序模型中使用的回归公式的详细信息。  
  
 通过查询模型内容可以提取时序模型的回归公式。 但是，若要查看完整的 ARTXP 或 ARIMA 公式，我们建议你使用**挖掘图例**的[Microsoft 时序查看器](browse-a-model-using-the-microsoft-time-series-viewer.md)，它能够以可读格式显示所有常量。  
  
 如果创建混合模型，则会在单独的树中创建 ARIMA 和 ARTXP 分析，并且在表示模型的根节点处联接。 RIMA 和 ARTXP 树的结构差异很大。 例如，ARTXP 树实际上是一种树结构，类似决策树，而 ARIMA 树则表示一系列移动平均值。 因此，尽管为方便起见而在一个模型中提供这两种表示形式，但应将它们视为两个独立的模型。 它们的公式也是完全不同的，因此不能进行组合或比较。  
  
 此外可以通过查看时序模型[Microsoft 一般内容树查看器](../microsoft-generic-content-tree-viewer-data-mining.md)。 时序模型的内容的详细信息，请参阅[时序模型的挖掘模型内容&#40;Analysis Services-数据挖掘&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)。  
  
### <a name="to-view-the-artxp-regression-formula-for-a-time-series-model"></a>查看时序模型的 ARTXP 回归公式  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，选择要查看的时序模型，然后单击 **“浏览”**。  
  
     --或者--  
  
     在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，选择该时序模型，然后单击 **“挖掘模型查看器”** 选项卡。  
  
2.  单击 **“模型”** 选项卡。  
  
3.  如果模型包含多个树，请从“树”下拉列表中选择一个树。  
  
    > [!NOTE]  
    >  您有多个数据序列时，模型将始终包含多个树。 但是，您在 **“时序查看器”** 中看到的树的数目却不像在 [Microsoft 一般内容树查看器](../microsoft-generic-content-tree-viewer-data-mining.md)中所看到的那么多。 这是因为时序查看器会将每个数据序列的 ARIMA 和 ARTXP 信息结合到单个表示形式中。  
  
4.  单击树中的任一叶节点。  
  
     标记为 **“数据序列”** 的节点始终为叶节点并且可包含公式。 如果“(全部)”节点没有子节点，则它也可包含一个公式。  
  
5.  如果未显示“挖掘图例”，请右键单击该节点，然后选择“显示图例”。  
  
     ARTXP 公式将在 **“挖掘图例”** 的前半部分显示为 **“树节点公式”**。  
  
### <a name="to-view-the-arima-formula-for-a-time-series-model"></a>查看时序模型的 ARIMA 公式  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，选择要查看的时序模型，然后单击 **“浏览”**。  
  
     --或者--  
  
     在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，选择该时序模型，然后单击 **“挖掘模型查看器”** 选项卡。  
  
2.  单击 **“模型”** 选项卡。  
  
3.  如果模型包含多个树，请从“树”下拉列表中选择一个树。  
  
    > [!NOTE]  
    >  当有多个数据序列时，模型将始终包含多个树。  
  
4.  单击树中的任一叶节点。  
  
     ARIMA 公式将在 **“挖掘图例”** 的后半部分显示为 **“ARIMA 公式”**。  
  
5.  如果未显示“挖掘图例”，请右键单击该节点，然后选择“显示图例”。  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型查看器任务和操作指南](mining-model-viewer-tasks-and-how-tos.md)   
 [使用 Microsoft 时序查看器浏览模型](browse-a-model-using-the-microsoft-time-series-viewer.md)   
 [时序模型查询示例](time-series-model-query-examples.md)  
  
  
