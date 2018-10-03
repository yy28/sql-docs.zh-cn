---
title: 分类向导 （Excel 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- classification [data mining]
ms.assetid: 409c5076-c4c3-4f09-8f30-d3297df45f13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ae0e86016d21e33507544747a44e5fc48b273ae2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094117"
---
# <a name="classify-wizard-data-mining-add-ins-for-excel"></a>分类向导（Excel 数据挖掘外接程序）
  ![数据挖掘功能区中的分类向导](media/dmc-classify.gif "数据挖掘功能区中的分类向导")  
  
 **分类**向导可帮助您生成基于 Excel 表、 Excel 区域或外部数据源中的现有数据的分类模型。  
  
 分类模型提取数据中表示相似性的模式，并帮助您基于值的分组进行预测。 例如，分类模型可用于根据收入或消费模式来预测风险。  
  
## <a name="using-the-classify-wizard"></a>使用分类向导  
  
1.  在中**数据挖掘**功能区中，单击**分类**，然后单击**下一步**。  
  
2.  在中**选择源数据**页上，选择要分析的数据。  
  
     此向导支持多种数据：Excel 表、Excel 区域和外部数据源。 对于外部数据，可以将其添加到 Excel 中，也可以在 Analysis Services 数据源中选择一组表或视图。 还可以添加表并更改列以创建临时数据源。  
  
3.  上**分类**页上，选择你想要分类的列。  
  
     查看在列表中，列**输入列**，并取消选择任何列具有唯一值，因此不是可用于创建模式，例如 ID 编号、 客户名称等。 您还应删除与可分类列基本重复的列。  
  
     举例来说，如果您要分类产品类别的预测，则在有已知业务规则时应排除子类别字段，否则此规则的强度可能会阻止您发现其他关联。  
  
4.  （可选） 单击**参数**可更改算法参数以及自定义聚类分析模型的行为。  
  
5.  在中**将数据拆分为定型集和测试集**页上，指定要为进行测试数据量。 剩余的数据始终用于定型模型。  
  
     默认设置为 30% 的测试数据和 70% 的定型数据。  
  
6.  上**完成**页上，提供你的数据集和模型的描述性名称并设置以下选项控制在完成的模型的使用方式：  
  
    -   **浏览模型**。 选中此选项后，尽快在向导完成处理模型，它会打开**浏览**窗口，从而帮助您浏览结果。 查看器的内容取决于您建立的模型的类型。 有关详细信息，请参阅[浏览决策树模型](browsing-a-decision-trees-model.md)并[浏览神经网络模型](browsing-a-neural-network-model.md)。  
  
    -   **启用钻取**。 选择此选项可以查看已完成模型中的基础数据。 此选项仅在建立决策树模型时可用。  
  
    -   **使用临时模型**。 如果您选择此选项，模型将不会被保存到服务器。 在您关闭 Excel 时，临时模型将被删除。  
  
## <a name="more-about-classification-models"></a>有关分类模型的详细信息  
 在中**算法参数**对话框中，您还可以选择从 Analysis Services 中提供这些算法的分类方法：  
  
-   Microsoft 决策树  
  
-   Microsoft 逻辑回归  
  
-   Microsoft Naïve Bayes  
  
-   Microsoft 神经网络  
  
 虽然多种算法可能会产生类似的结果，但是它们分析数据的方式不同，因此，我们建议尝试几种算法并比较结果。 默认方法是 Microsoft 决策树。  
  
 在中**参数**列表中，可以更改高级的选项，取决于您选择的算法类型。 每种算法的参数在 SQL Server 联机丛书中有更详细的说明。  
  
 [Microsoft 决策树算法技术参考](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Microsoft 逻辑回归算法技术参考](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Microsoft Naive Bayes 算法技术参考](data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)  
  
 [Microsoft 神经网络算法技术参考](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>要求  
 若要使用**分类**向导，您必须连接到[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据库。 有关如何创建连接的信息，请参阅[连接到源数据&#40;Excel 数据挖掘客户端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。  
  
## <a name="see-also"></a>请参阅  
 [创建数据挖掘模型](creating-a-data-mining-model.md)  
  
  
