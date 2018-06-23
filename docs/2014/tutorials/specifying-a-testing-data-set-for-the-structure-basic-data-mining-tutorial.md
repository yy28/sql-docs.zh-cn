---
title: 指定测试数据集结构 （数据挖掘基础教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 75cd508f-b126-418b-848d-3c4c3e6c303f
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2023672b21e8ffde191b400329031895d200e1ea
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312625"
---
# <a name="specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial"></a>为结构指定测试数据集（数据挖掘基础教程）
  在数据挖掘向导的最后几个屏幕上，将把数据拆分成测试集和定型集。 随后您将命名您的结构并针对模型启用钻取。  
  
## <a name="specifying-a-testing-set"></a>指定测试集  
 在创建挖掘结构时将数据分成定型集和测试集，可以轻松地评估以后创建的挖掘模型的准确性。 测试集的详细信息，请参阅[定型集和测试数据集](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
#### <a name="to-specify-the-testing-set"></a>若要指定测试集  
  
1.  上**创建测试集**页上，为**的数据以供测试百分比**，保留默认值为`30`。  
  
2.  有关**中测试数据集中的事例的最大数目**，类型`1000`。  
  
3.  单击“下一步” 。  
  
## <a name="specifying-drillthrough"></a>指定钻取  
 可以针对模型和结构启用钻取。 此对话框中的复选框可对命名模型启用钻取功能。 在处理了该模型后，您将能够从定型数据中检索用于创建模型的详细信息。  
  
 如果基础挖掘结构也已经配置为允许进行钻取，则可以从模型事例和挖掘结构返回详细信息（其中包括挖掘模型中所不包含的列）。 有关详细信息，请参阅[钻取查询（数据挖掘）](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
#### <a name="to-name-the-model-and-structure-and-specify-drillthrough"></a>命名模型和结构并指定钻取  
  
1.  上**完成向导**页上，在**挖掘结构名称**，类型`Targeted Mailing`。  
  
2.  在**挖掘模型名称**，类型`TM_Decision_Tree`。  
  
3.  选择**允许钻取**复选框。  
  
4.  查看**预览**窗格。 请注意，只能选择作为这些列**密钥**，**输入**或**可预测**显示。 您选择的其他列（例如，AddressLine1）不能用于生成模型，但是将在基础结构中可用，您可以在处理和部署模型之后查询这些列。  
  
5.  单击 **“完成”**。  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [指定的数据类型和内容类型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一课  
 [第 3 课：添加和处理模型](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="see-also"></a>请参阅  
 [为挖掘模型启用钻取](../../2014/analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)   
 [钻取查询&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [指定定型数据&#40;数据挖掘向导&#41;](../../2014/analysis-services/specify-the-training-data-data-mining-wizard.md)  
  
  