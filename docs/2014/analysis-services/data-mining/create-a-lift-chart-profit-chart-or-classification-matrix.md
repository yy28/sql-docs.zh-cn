---
title: 创建提升图、 利润图或分类矩阵 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services], mining structures
ms.assetid: aa3d052f-58a9-4417-8e7a-5e6feb562af0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e183c1e25aa81b05c897674fc5c9f4a2dd8d0c5b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529358"
---
# <a name="create-a-lift-chart-profit-chart-or-classification-matrix"></a>创建提升图、利润图或分类矩阵
  可以使用五个基本步骤为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据挖掘模型创建准确性图表：  
  
-   选择包含要比较的挖掘模型的挖掘结构。  
  
-   选择要添加到图表中的挖掘模型。  
  
-   指定要在生成图表的过程中使用的测试数据的源。  
  
-   选择图表类型。  
  
-   配置图表选项。  
  
 对于提升图、利润图和分类矩阵而言，这些基本步骤是相同的。 下面的过程概述了为这些图表类型配置基本图表选项的步骤。 有关如何创建交叉验证报表的信息，请参阅 [交叉验证报表中的度量值](measures-in-the-cross-validation-report.md)。  
  
### <a name="open-the-mining-structure-in-the-accuracy-chart-designer"></a>在准确性图表设计器中打开挖掘结构  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开数据挖掘设计器。  
  
2.  在解决方案资源管理器中，双击包含挖掘模型的结构。  
  
3.  单击 **“挖掘准确性图表”** 选项卡。  
  
### <a name="select-mining-models-for-inclusion-in-the-chart"></a>选择要包括在图表中的挖掘模型  
  
1.  在 **中的数据挖掘设计器的** “挖掘准确性图表” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡上，单击 **“输入选择”** 选项卡。  
  
     其中的列表显示了当前结构中具有相同可预测属性的所有模型。  
  
2.  对要包括在图表中的每个模型选中 **“显示”** 框。  
  
3.  单击 **“可预测列名称”** 文本框，从列表中选择可预测列的名称。 放入一个图表中的所有模型都必须具有相同的可预测列。  
  
4.  如果您比较两个模型，但其可预测列具有不同的值或不同的数据类型，则应清除 **“同步预测列和值”** 框以强制进行比较。  
  
    > [!NOTE]  
    >  如果选中了 **“同步预测列和值”** 框，则 Analysis Services 会分析模型的可预测列中的数据和测试数据，并尝试找到最佳匹配项。 因此，除非绝对需要强制进行列的比较，否则不要清除此框。  
  
5.  单击 **“预测值”** 文本框，并从列表中选择一个值。 如果可预测列是连续数据类型，则必须在此文本框中键入一个值。  
  
     有关详细信息，请参阅 [选择用于测试挖掘模型的列](choose-the-column-to-use-for-testing-a-mining-model.md)。  
  
### <a name="select-testing-data"></a>选择测试数据  
  
1.  在 **“挖掘准确性图表”** 选项卡的 **“输入选择”** 选项卡上，通过选择 **“选择要用于准确性图表的数据集”** 组中的一个选项来指定将用来生成图表的数据源。  
  
    -   如果您想要使用挖掘结构测试事例和在模型创建期间可能已应用的任何筛选器的交集定义的事例的子级，则选择选项 **“使用挖掘模型测试事例”**。  
  
    -   选择 **“使用挖掘结构测试事例”** 选项可以使用已作为挖掘结构维持数据集的一部分定义的测试事例的完整集合。  
  
    -   若要使用外部数据，请选择“指定其他数据集”选项。   数据集必须可用作数据源视图。   单击浏览 (**...**) 按钮以选择要用于准确性图表的数据表。 有关详细信息，请参阅 [Choose and Map Model Testing Data](choose-and-map-model-testing-data.md)。  
  
         如果您使用的是外部数据集，则可以选择筛选输入数据集。 有关详细信息，请参阅 [将筛选器应用于模型测试数据](apply-filters-to-model-testing-data.md)。  
  
> [!NOTE]  
>  不能在 **“输入选择”** 选项卡上的模型测试事例或挖掘结构测试事例上创建筛选器。若要在挖掘模型上创建筛选器，应修改该模型的“筛选器”属性。 有关详细信息，请参阅 [对挖掘模型应用筛选器](apply-a-filter-to-a-mining-model.md)。  
  
### <a name="configure-chart-settings-and-generate-the-chart"></a>配置图表设置并生成图表  
  
1.  在 **“挖掘准确性图表”** 选项卡中，单击要创建的图表的对应选项卡。  
  
2.  对于提升图 ，请单击 **“提升图”** 选项卡。图表将基于模型、可预测属性以及您刚选择的输入数据自动生成。  
  
3.  对于分类矩阵 ，请单击 **“分类矩阵”** 选项卡。无需进一步的设置；图表将基于输入数据以及您选择的模型自动生成。  
  
4.  对于利润图 ，请首先单击 **“提升图”** 选项卡。然后，从“图表类型”下拉列表中选择“利润图”。  
  
     在 **“利润图设置”** 对话框中输入以下设置。  
  
     **人口数**  
     创建提升图时要使用的数据集中的事例数。  
  
     该模型总是按概率降低的顺序选择事例，也就是说，如果正在评估潜在客户并且选择的数字仅表示客户数据库中记录数的一半，则该模型将在最适合于您的模型的事例子集上度量准确性。  
  
     这是因为当使用该模型生成邮件或者创建活动时，将使用与每个事例关联的预测概率，以仅针对做出积极响应的概率最大的那些客户。  
  
     **固定成本**  
     与业务问题关联的固定成本。  
  
     如果针对的是目标邮递解决方案，则固定成本可能表示打印机设置费用，其中包含准备促销邮件的初始成本。  
  
     此成本一次性应用于整个目标总体。  
  
     **单项成本**  
     除固定成本之外的成本，可以与每个客户联系相关联。 例如，可以输入促销邮件的邮费或者打电话的成本。  
  
     此成本必须与整体目标总体相同。 每个值与目标事例数相乘。  
  
     **单项收入**  
     与每个成功销售相关联的收入金额。  
  
## <a name="see-also"></a>请参阅  
 [提升图（Analysis Services - 数据挖掘）](lift-chart-analysis-services-data-mining.md)   
 [分类矩阵（Analysis Services - 数据挖掘）](classification-matrix-analysis-services-data-mining.md)  
  
  
