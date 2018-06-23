---
title: 修改和处理市场篮模型 （数据挖掘中级教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b6019413-aebd-4ff7-831a-644572ad88b1
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 96eb44713cd34fdcea81a7e5e4daf26739afdec1
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36311905"
---
# <a name="modifying-and-processing-the-market-basket-model-intermediate-data-mining-tutorial"></a>修改和处理市场篮模型（数据挖掘中级教程）
  在处理你创建的关联挖掘模型之前，你必须更改的两个参数的默认值：*支持*和*概率*。  
  
-   *支持*定义的顺序，才会被认为有效必须存在的规则的事例的百分比。 您将指定规则必须至少是在百分之一的事例中发现的。  
  
-   *概率*定义关联的必须如何可能被视为有效之前保留。 您将认为任何关联都必须具有至少百分之十的可能性。  
  
 增加或减少支持和概率的效果的详细信息，请参阅[Microsoft Association Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)。  
  
 你定义的结构和参数之后**关联**挖掘模型，你将处理该模型。  
  
### <a name="to-adjust-the-parameters-of-the-association-model"></a>调整 Association 模型的参数  
  
1.  打开**挖掘模型**数据挖掘设计器选项卡。  
  
2.  右键单击**关联**在设计器，选择网格中的列**设置算法参数，以打开算法参数**对话框。  
  
3.  在**值**列**算法参数**对话框框中，设置以下参数：  
  
     MINIMUM_PROBABILITY = 0.1  
  
     MINIMUM_SUPPORT = 0.01  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-process-the-mining-model"></a>若要处理挖掘模型  
  
1.  上**挖掘模型**菜单[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，选择**处理挖掘结构和所有模型。**  
  
2.  警告询问是否要生成并部署项目时，请单击**是**。  
  
     **处理挖掘结构的关联**对话框随即打开。  
  
3.  单击 **“运行”**。  
  
     **处理进度**对话框将打开以显示有关模型处理的信息。 处理新的结构和模型可能需要一些时间。  
  
4.  处理完成后，单击**关闭**退出**处理进度**对话框。  
  
5.  单击**关闭**再次以退出**处理挖掘结构的关联**对话框。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [浏览市场篮模型&#40;中间数据挖掘教程&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [处理要求和注意事项&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  