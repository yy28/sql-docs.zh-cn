---
title: 修改和处理市场篮模型（数据挖掘中级教程） |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63301364"
---
# <a name="modifying-and-processing-the-market-basket-model-intermediate-data-mining-tutorial"></a>修改和处理市场篮模型（数据挖掘中级教程）
  在处理创建的关联挖掘模型之前，必须更改以下两个参数的默认值：*支持*和*概率*。  
  
-   *支持*定义规则在被视为有效前必须存在的事例的百分比。 您将指定规则必须至少是在百分之一的事例中发现的。  
  
-   *概率*定义了关联在被视为有效之前必须具备的可能性。 您将认为任何关联都必须具有至少百分之十的可能性。  
  
 有关增加或降低支持和概率的影响的详细信息，请参阅[Microsoft 关联算法技术参考](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)。  
  
 在定义了**关联**挖掘模型的结构和参数后，您将处理该模型。  
  
### <a name="to-adjust-the-parameters-of-the-association-model"></a>调整 Association 模型的参数  
  
1.  打开数据挖掘设计器的 "**挖掘模型**" 选项卡。  
  
2.  在设计器中右键单击网格中的 "**关联**" 列，然后选择 **"设置算法参数" 以打开 "算法参数"** 对话框。  
  
3.  在 "**算法参数**" 对话框的 "**值**" 列中，设置以下参数：  
  
     MINIMUM_PROBABILITY = 0.1  
  
     MINIMUM_SUPPORT = 0.01  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-process-the-mining-model"></a>处理挖掘模型  
  
1.  在的[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]"**挖掘模型**" 菜单上，选择 "**处理挖掘结构和所有模型"。**  
  
2.  如果出现警告，询问您是否要生成和部署项目，请单击 **"是"**。  
  
     "**处理挖掘结构-关联**" 对话框将打开。  
  
3.  单击“运行”****。  
  
     "**处理进度**" 对话框将打开以显示有关模型处理的信息。 处理新的结构和模型可能需要一些时间。  
  
4.  处理完成后，单击 "**关闭**" 退出 "**处理进度**" 对话框。  
  
5.  再次单击 "**关闭**" 以退出 "**处理挖掘结构-关联**" 对话框。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [&#40;中级数据挖掘教程了解市场篮模型&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [处理要求和注意事项（数据挖掘）](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
