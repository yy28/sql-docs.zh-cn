---
title: 修改和处理市场篮模型 （数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b6019413-aebd-4ff7-831a-644572ad88b1
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4987e3497b7d52ff11f8f52bc403105340f7f508
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63301364"
---
# <a name="modifying-and-processing-the-market-basket-model-intermediate-data-mining-tutorial"></a>修改和处理市场篮模型（数据挖掘中级教程）
  在处理你创建的关联挖掘模型之前，必须更改两个参数的默认值：*支持*并*概率*。  
  
-   *支持*定义在其中，被视为有效前必须存在的规则的事例的百分比。 您将指定规则必须至少是在百分之一的事例中发现的。  
  
-   *概率*定义可能性关联必须先被视为有效。 您将认为任何关联都必须具有至少百分之十的可能性。  
  
 增加或减少支持和概率的效果的详细信息，请参阅[Microsoft 关联算法技术参考](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)。  
  
 在定义的结构和参数之后**关联**挖掘模型，将处理该模型。  
  
### <a name="to-adjust-the-parameters-of-the-association-model"></a>调整 Association 模型的参数  
  
1.  打开**挖掘模型**数据挖掘设计器选项卡。  
  
2.  右键单击**关联**在设计器中，选择网格中的列**设置算法参数，以打开算法参数**对话框。  
  
3.  在中**值**的列**算法参数**对话框框中，设置以下参数：  
  
     MINIMUM_PROBABILITY = 0.1  
  
     MINIMUM_SUPPORT = 0.01  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-process-the-mining-model"></a>处理挖掘模型  
  
1.  上**挖掘模型**菜单[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，选择**处理挖掘结构和所有模型。**  
  
2.  在警告，询问您是否要生成并部署项目，单击**是**。  
  
     **处理挖掘结构-Association**对话框随即打开。  
  
3.  单击 **“运行”**。  
  
     **处理进度**对话框将打开以显示有关模型处理的信息。 处理新的结构和模型可能需要一些时间。  
  
4.  处理完成后，单击**关闭**退出**处理进度**对话框。  
  
5.  单击**关闭**再次以退出**处理挖掘结构-Association**对话框。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [浏览市场篮模型&#40;数据挖掘中级教程&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [处理要求和注意事项（数据挖掘）](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
