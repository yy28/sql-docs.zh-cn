---
title: 创建相关的顺序分析和聚类分析模型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1fb4f5bc-1756-45ca-9cd7-411a8c5992a9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 71db7ba5246e151bbca8a52972a2ba835b80ddb6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62855869"
---
# <a name="creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial"></a>创建相关的顺序分析和聚类分析模型（数据挖掘中级教程）
  通过浏览顺序分析和聚类分析模型，您了解到如 Region 或 Income 等其他属性对模型有巨大影响；因此为了更好地了解序列，您将创建一个相关的顺序分析和聚类分析模型，并删除与客户人口统计信息有关的属性。  
  
 在本任务中，您将创建区域顺序分析和聚类分析模型的副本，然后从该模型中删除与序列没有直接关系的任何列。  
  
 新模型包含的所有列与它所基于的挖掘模型的列相同。 但是，您不需要删除挖掘结构中的列，只需指定新挖掘模型忽略这些列即可。  
  
### <a name="to-make-a-copy-of-the-sequence-clustering-model"></a>创建顺序分析和聚类分析模型的副本  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的数据挖掘设计器中，单击 "**挖掘模型**" 选项卡。  
  
2.  右键单击要复制的模型，然后选择 "**新建挖掘模型**"。  
  
3.  在 "**新建挖掘模型**" 对话框中，键入模型名称，然后选择 " `Sequence Clustering`Microsoft"。  
  
     对于本教程，请键入名称`Sequence Clustering`。  
  
4.  单击“确定”。   
  
### <a name="to-remove-columns-from-the-mining-model"></a>从挖掘模型中删除列  
  
1.  在 "**挖掘模型**" 选项卡中，在名为 "序列聚类分析" 的新模型的列中，单击 "**收入组**" 属性所在的行，然后选择 "**忽略**"。  
  
2.  为属性**区域**重复此步骤。  
  
3.  单击表名称旁边的加号 " **v Assoc Seq 行项**"，展开表并查看嵌套表中的列。  
  
     新模型应该仅有以下列：  
  
     **订单 NumberKey**  
  
     **行号键**  
  
     **模型预测**  
  
### <a name="to-process-the-new-sequence-clustering-model"></a>处理新的顺序分析和聚类分析模型  
  
1.  在 "**挖掘模型**" 选项卡中，右键单击名为`Sequence Clustering`的新模型，然后选择 "**处理模型**"。  
  
     由于该新的简化挖掘模型基于已经处理过的结构，因此您不需要再重新处理该结构。 您只需处理该新的挖掘模型。  
  
2.  单击 **"是"** 将更新后的数据挖掘项目部署到服务器。  
  
3.  在 "**处理挖掘模型**" 对话框中，单击 "**运行**"。  
  
4.  单击 "**关闭**" 关闭 "**处理进度**" 对话框，然后再次单击 "**处理挖掘模型**" 对话框中的 "**关闭**"。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [对顺序分析和聚类分析模型创建预测 &#40;中间数据挖掘教程&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘 &#40;处理要求和注意事项&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
