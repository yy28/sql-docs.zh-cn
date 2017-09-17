---
title: "应用筛选器以测试数据创建模型 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input row filtering [SQL Server]
- filtering input rows [Analysis Services]
- Mining Accuracy Chart [Analysis Services], filtering input rows
ms.assetid: 9ccc9a23-5597-4b35-a05f-2fc8eb885147
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ae4d7899d0b027f912b6320934ddefc2431a303a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="apply-filters-to-model-testing-data"></a>将筛选器应用于模型测试数据
  在指定测试模型时使用的外部数据源时，可以选择应用筛选器以限制输入数据。 例如，您可能想要专门针对有关某一收入范围的客户的预测来测试模型。  
  
 例如，在 Adventure Works 目标邮件方案中，你可以对 ProspectiveBuyer（这是包含测试数据的表）创建一个如下的筛选表达式并按收入范围来限制测试事例：  
  
 `[YearlyIncome] = '50000'`  
  
 根据您是在筛选定型数据还是测试数据集，筛选器的行为稍有不同：  
  
-   在对测试数据集定义筛选器时，将对传入数据创建一个 WHERE 子句。 如果要筛选用于评估模型的输入数据集，则在创建图表时筛选表达式将转换为 Transact-SQL 语句并应用于输入表。 结果，测试事例数会大大减少。  
  
-   在对挖掘模型应用筛选器时，所创建的筛选表达式将转换为数据挖掘扩展插件 (DMX) 语句并应用于单个模型。 因此，在对模型应用筛选器时，只有原始数据的子集用于定型该模型。 如果您使用一组条件筛选定型模型，以便模型优化为某一组数据，然后使用另一组条件对模型进行测试，这可能会导致问题。  
  
-    如果创建结构时定义了测试数据集，则用于定型的模型事例将仅包括挖掘结构定型集中满足筛选条件的那些事例。 因此，在您测试模型并且选择 **“使用挖掘模型测试事例”**选项时，测试事例将仅包括挖掘结构测试集中满足筛选条件的事例。 但是，如果未定义维持数据集，用于测试的模型事例将包括该数据集中满足筛选条件的所有事例。  
  
-   您对模型应用的筛选条件也会影响对模型事例的钻取查询。  
  
 总之，在您测试多个模型时，即使所有模型都基于相同的挖掘结构，您也必须了解这些模型可能会使用不同的数据子集来进行定型和测试。 这可能对准确性图表具有以下影响：  
  
-   测试集中事例的总数在要测试的各模型中可能会不同。  
  
-   如果模型使用不同的定型数据或测试数据的子集，则每个模型的百分比在图表中可能不会对齐。  
  
 为了确定某一模型是否包含可能会影响结果的预定义筛选器，您可以在 **“属性”** 窗格中查找 **Filter** 属性，或者可以通过使用数据挖掘架构行集对模型进行查询。 例如，下面的查询将返回指定模型的筛选器文本：  
  
 `SELECT [FILTER] FROM $system.DMSCHEMA_MINING_MODELS WHERE MODEL_NAME = 'name of model’`  
  
> [!WARNING]  
>  如果您想要从现有挖掘模型中删除筛选器或更改筛选条件，则必须重新处理该挖掘模型。  
  
 有关可以应用的筛选器类型以及如何计算筛选表达式的详细信息，请参阅[模型筛选器语法和示例（Analysis Services – 数据挖掘）](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)。  
  
### <a name="create-a-filter-on-external-testing-data"></a>创建针对外部测试数据的筛选器  
  
1.  双击包含您要测试的模型的挖掘结构，以便打开数据挖掘设计器。  
  
2.  选择“挖掘准确性图表”  选项卡，然后选择“输入选择”  选项卡。  
  
3.  在“输入选择”  选项卡的“选择要用于准确性图表的数据集” 下，选择“指定其他数据集” 选项。  
  
4.  单击浏览按钮“(…)”以打开一个对话框，并选择外部数据集。  
  
5.  选择事例表，并根据需要添加嵌套表。 根据需要将模型中的列映射到外部数据集中的列。 关闭 **“指定列映射”** 对话框以便保存源表定义。  
  
6.  单击 **“打开筛选器编辑器”** 为数据集定义筛选器。  
  
     此时将打开 **“数据集筛选器”** 对话框。 如果结构包含嵌套表，则可以分两部分创建筛选器。 首先，使用 **“数据集筛选器”** 对话框对事例表设置条件，然后使用 **“筛选器”** 对话框对嵌套行设置条件。  
  
7.  在 **“数据集筛选器”** 对话框中，单击网格顶部的行，并在 **“挖掘结构列”**下的列表中选择表或列。  
  
     如果数据源视图包含多个表或一个嵌套表，则必须先选择表名。 如果不先选择表名，则还可以直接从事例表中选择列。  
  
     为需要进行筛选的每个列都添加一个新行。  
  
8.  使用 **“运算符”**和 **“值”** 列来定义列的筛选方式。  
  
     **注意** ：键入值时不必使用引号。  
  
9. 单击“和/或”文本框并选择逻辑运算符来定义多个条件的组合方式。  
  
10. 还可以根据需要单击“值”文本框右侧的浏览按钮“(…)”，以打开“筛选器”对话框，并对嵌套表或单个事例表列设置条件。  
  
11. 查看 **“表达式”** 窗格中的文本以验证整个筛选器条件是否正确。  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     筛选器条件将在创建准确性图表时应用到数据源。  
  
## <a name="see-also"></a>另请参阅  
 [选择和映射模型测试数据](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)   
 [使用嵌套表数据作为输入准确性图表](../../analysis-services/data-mining/using-nested-table-data-as-an-input-for-an-accuracy-chart.md)   
 [选择准确性图表类型和设置图表选项](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  
