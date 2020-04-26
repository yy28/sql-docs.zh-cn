---
title: 在目标邮件结构中处理模型（数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9d8233bb-117e-4563-9302-8a5a8ad1fae2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 605088d405cbd2dcfba92a2da5fa4e07c38d8f0b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63188224"
---
# <a name="processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>处理 Targeted Mailing 结构中的模型（数据挖掘基础教程）
  必须先部署 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目并处理挖掘结构和挖掘模型，然后才能浏览或使用创建的挖掘模型。  
  
-   *部署*将项目发送到服务器，并在服务器上创建该项目中的所有对象。  
  
-   *处理*将[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]用关系数据源中的数据填充对象。  
  
 模型经过部署和处理后才能使用。 此外，当您对模型进行任何更改（如添加新数据）时，必须重新部署和重新处理模型。  
  
## <a name="ensuring-consistency-with-holdoutseed"></a>确保与 HoldoutSeed 一致  
 部署项目并处理结构和模型后，将数据结构中的各行根据数值种子值分配给定型集或测试集。 默认情况下，数值种子值是根据数据结构的属性计算的。 但是，如果您更改过模型的某些方面，该种子值将变化，导致结果略有不同。 因此，为了确保您的结果与此处所述的结果相同，我们将随机分配固定的`12`*维持种子*。 维持种子用来初始化抽样算法的种子，并确保以大体相同的方式对所有挖掘结构及其模型中的数据进行分区。  
  
 此值不影响定型集内的事例数，它仅确保每次生成模型时将使用相同的分区方法。  
  
 有关维持种子的详细信息，请参阅[定型和测试数据集](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
#### <a name="to-set-the-holdout-seed"></a>设置维持种子  
  
1.  在的数据挖掘设计器中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]单击 "**挖掘结构**" 选项卡或 "**挖掘模型**" 选项卡。  
  
     **目标邮件 MiningStructure**显示在 "**属性**" 窗格中。  
  
2.  通过按**F4**确保 "**属性**" 窗格处于打开状态。  
  
3.  确保将**CacheMode**设置为**KeepTrainingCases**。  
  
4.  为`12` **HoldoutSeed**输入。  
  
## <a name="deploying-and-processing-the-models"></a>部署并处理模型  
 在数据挖掘设计器中，您可以决定要处理的对象，具体取决于您对模型或基础数据所做的更改的范围：  
  
 在本任务中，因为数据和模型是新的，我们将同时处理结构和所有模型。  
  
#### <a name="to-deploy-the-project-and-process-all-the-mining-models"></a>部署项目并处理所有挖掘模型  
  
1.  在 "**挖掘模型**" 菜单中，选择 "**处理挖掘结构和所有模型**"。  
  
     如果更改了结构，系统将提示您在处理模型之前生成和部署项目。 单击 **“是”** 。  
  
2.  在 "**处理挖掘结构-目标邮件**" 对话框中，单击 "**运行**"。  
  
     **“处理进度”** 对话框将打开以显示有关模型处理的详细信息。 模型处理可能需要一些时间，具体取决于您的计算机。  
  
3.  模型处理完成后，在 **“处理进度”** 对话框中单击 **“关闭”** 。  
  
4.  在 "**处理挖掘结构- \<结构>** " 对话框中单击 "**关闭**"。  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [将新模型添加到目标邮件结构 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一课  
 [第4课：浏览目标邮件模型 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [处理要求和注意事项（数据挖掘）](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
