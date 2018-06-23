---
title: 创建相关的序列聚类分析模型 （数据挖掘中级教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1fb4f5bc-1756-45ca-9cd7-411a8c5992a9
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c0820b087583194e78af1d1de46b4affe3a1d9fc
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36311805"
---
# <a name="creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial"></a>创建相关的顺序分析和聚类分析模型（数据挖掘中级教程）
  通过浏览顺序分析和聚类分析模型，您了解到如 Region 或 Income 等其他属性对模型有巨大影响；因此为了更好地了解序列，您将创建一个相关的顺序分析和聚类分析模型，并删除与客户人口统计信息有关的属性。  
  
 在本任务中，您将创建区域顺序分析和聚类分析模型的副本，然后从该模型中删除与序列没有直接关系的任何列。  
  
 新模型包含的所有列与它所基于的挖掘模型的列相同。 但是，您不需要删除挖掘结构中的列，只需指定新挖掘模型忽略这些列即可。  
  
### <a name="to-make-a-copy-of-the-sequence-clustering-model"></a>创建顺序分析和聚类分析模型的副本  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，在数据挖掘设计器中，单击**挖掘模型**选项卡。  
  
2.  右键单击你想要复制和选择的模型**新建挖掘模型**。  
  
3.  在**新建挖掘模型**对话框中，键入模型名称，然后选择 Microsoft `Sequence Clustering`。  
  
     对于本教程中，键入名称`Sequence Clustering`。  
  
4.  单击“确定” 。  
  
### <a name="to-remove-columns-from-the-mining-model"></a>从挖掘模型中删除列  
  
1.  在**挖掘模型**选项卡上，为新模型名为序列聚类分析，列中的单击对应的行**收入组**属性，然后选择**忽略**。  
  
2.  属性重复此步骤**区域**。  
  
3.  单击表名旁边的加号**v 关联 Seq 行项**，若要展开的表，然后查看嵌套表中的列。  
  
     新模型应该仅有以下列：  
  
     **顺序 NumberKey**  
  
     **行数字键**  
  
     **模型预测**  
  
### <a name="to-process-the-new-sequence-clustering-model"></a>处理新的顺序分析和聚类分析模型  
  
1.  在**挖掘模型**选项卡上，右键单击名为的新模型`Sequence Clustering`，然后选择**进程模型**。  
  
     由于该新的简化挖掘模型基于已经处理过的结构，因此您不需要再重新处理该结构。 您只需处理该新的挖掘模型。  
  
2.  单击**是**将更新后的数据挖掘项目部署到服务器。  
  
3.  在**处理挖掘模型**对话框中，单击**运行**。  
  
4.  单击**关闭**关闭**处理进度**对话框中，然后单击**关闭**再次在**处理挖掘模型**对话框。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [在聚类分析模型的序列上创建预测&#40;中间数据挖掘教程&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [处理要求和注意事项&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  