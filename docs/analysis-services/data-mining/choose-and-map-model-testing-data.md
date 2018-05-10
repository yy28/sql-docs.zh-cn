---
title: 选择和映射模型测试数据 |Microsoft 文档
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d74352fcb3564eda40257430ff442f622fcec89e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="choose-and-map-model-testing-data"></a>选择和映射模型测试数据
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  若要在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中创建准确性图表，您必须选择将用于测试模型的数据，并且将数据映射到模型。  
  
 默认情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用挖掘模型测试数据，只要在生成挖掘结构时创建了维持数据集。 创建维持测试集是测试基于相同挖掘结构的模型的最简单方式，因为列名和数据类型将始终与该模型匹配，并且您可以合理地确定数据分布是相似的。 此外，设计器将自动创建输入和模型列之间的关系。  
  
 或者，您可以指定外部数据源。 对于外部数据，有一些其他要求：  
  
-   外部数据集必须定义为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例中的数据源视图。  
  
-   外部数据集必须至少包含一个可映射到挖掘模型中可预测列的列。 可以选择忽略某些列。  
  
-   不能在另一个数据源视图中添加新列或映射列。 选择的数据源视图必须包含预测查询所需的所有列。  
  
-   如果外部列名称与模型中的列名称完全匹配，则设计器将自动映射这些列。 如果映射是错误的，您可以更改这些映射，或者删除它们并为现有列创建新映射。  
  
-   如果您使用外部数据源，则可以应用筛选器以将测试数据限制为事例的相关子集。  
  
-   即使在使用维持测试集时，您也应知道筛选器可能在与挖掘结构关联的测试数据和挖掘模型测试事例之间导致差异。  
  
 本主题描述如何选择和映射测试数据：  
  
 [选择输入表以测试挖掘模型的准确性](#bkmk_SelectInputs)  
  
 [将输入列映射到测试数据中的列](#bkmk_MapColumns)  
  
 [更改测试数据中的列映射到模型的方式](#bkmk_ChangeMappings)  
  
##  <a name="bkmk_SelectInputs"></a> 选择输入表以测试挖掘模型的准确性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的数据挖掘设计器中，双击包含要制作图表的模型的挖掘结构。  
  
2.  选择 **“挖掘准确性图表”** 选项卡。  
  
3.  在 **“挖掘准确性图表”** 视图的 **“输入选择”** 选项卡中，选择下面的选项之一：  
  
     **使用挖掘模型测试事例**  
  
     **使用挖掘结构测试事例**  
  
     **指定其他数据集**  
  
4.  如果您选择的是 **“指定其他数据集”**，则可以选择单击 **“打开筛选器编辑器”** 来针对输入数据集创建筛选条件。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  单击 **“提升图”** 选项卡或 **“分类矩阵”** 选项卡，使用指定的测试数据自动生成该图表。  
  
##  <a name="bkmk_MapColumns"></a> 将模型列映射到测试数据中的列  
  
1.  双击包含要建立图表的模型的挖掘结构，以在数据挖掘设计器中打开结构和模型。  
  
2.  选择“挖掘准确性图表”  选项卡，然后选择“输入选择”  选项卡。  
  
3.  在 **“输入选择”** 选项卡中的 **“选择要用于准确性图表的数据集”**下，选择 **“指定其他数据集”**。  
  
4.  单击浏览按钮 **(…)** 以打开一个对话框，并生成外部数据集的定义。  
  
5.  在 **“选择挖掘结构”** 对话框中，选择包含您要使用的模型的挖掘结构，然后单击 **“确定”**。  
  
6.  在“挖掘准确性图表”选项卡的“选择输入表”表上，单击“选择事例表”以打开“选择表”对话框。  
  
7.  在 **“选择表”** 对话框中，从 **“数据源”** 列表中选择数据源。 选择一个表，其中包含预测查询中要用来确定模型准确性的数据。  
  
8.  在“表/视图名称”框中，选择包含要用来测试模型的数据的表。  
  
9. 根据需要编辑映射。 挖掘结构中的列将自动映射到输入表中具有相同名称的列。 若要手动创建映射，请单击“选择输入表”表中的列并将它拖到“挖掘结构”表中相应的列。 若要删除映射，请单击将“挖掘结构”表中的列链接到“选择输入表”表中的映射列的行，然后按 Delete。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="bkmk_ChangeMappings"></a> 修改输入数据映射到模型的方式  
  
1.  在数据挖掘设计器中，双击包含要制作图表的模型的结构。  
  
2.  选择 **“挖掘准确性图表”** 选项卡。  
  
3.  单击 **“输入选择”** 选项卡。  
  
4.  在 **“选择要用于准确性图表的数据集”**中，选择 **“指定其他数据集”**选项。  
  
5.  单击浏览按钮 **(…)** 打开一个对话框并生成外部数据源的定义。  
  
6.  在 **“指定列映射”** 对话框中，单击 **“选择事例表”**。  
  
7.  在“选择表”对话框中，从列表中选择数据源视图，然后选择包含事例数据的表。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  如果所需的表不可用，则关闭该对话框，然后创建一个包含该表的新的数据源视图。 有关如何创建数据源视图的信息，请参阅[定义数据源视图 (Analysis Services)](../../analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services.md)。  
  
9. 如果挖掘模型包含嵌套表，则单击 **“选择嵌套表”**，然后从数据源视图的表的列表中选择该嵌套表。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. 选择要修改的映射的联接线，然后选择 **“修改连接”**。  
  
     此时，将打开 **“修改映射”** 对话框。 在此对话框的表中， **“挖掘结构列”** 列出了所选挖掘结构包含的每个列； **“表列”** 列出了输出表中的列，这些列映射到挖掘结构中的列。  
  
11. 在 **“表列”**下，选择与要修改其关系的 **“挖掘结构列”** 下的行对应的行。 从列表中选择一个新列，或者从列表中选择空白项以删除该列。  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     **“指定列映射”** 对话框中将显示新的列映射。 通过选择列之间的连线，然后按 Delete 键，可以删除映射。 通过在“挖掘结构”表中选择列，然后将其拖到“选择输入表”表中的对应列，可以创建一个新连接。  
  
## <a name="see-also"></a>另请参阅  
 [测试和验证任务和操作指南 & #40; 数据挖掘 & #41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
  
