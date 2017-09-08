---
title: "挖掘模型的筛选器 (Analysis Services-数据挖掘) |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attributes [data mining]
- filter syntax [data mining]
- models [Analysis Services], filtering
- filters [data mining]
- filtering data [Analysis Services]
ms.assetid: 0f29c19c-4be3-4bc7-ab60-f4130a10d59c
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: db42f50eca097c58afac1ded71d143f8230fd42d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="filters-for-mining-models-analysis-services---data-mining"></a>挖掘模型的筛选器（Analysis Services - 数据挖掘）
  基于数据的模型筛选有助于创建利用挖掘结构中的数据子集的挖掘模型。 使用筛选功能，可以基于全面的数据源视图来创建单个挖掘结构，因此可以灵活地设计挖掘结构和数据源。 随后即可以创建筛选器，以便仅将该数据的一部分用于对各种模型进行定型和测试，而不是为数据的每个子集均生成不同的结构和相关模型。  
  
 例如，针对 Customers 表和相关表定义数据源视图。 随后，定义一个包括所需的全部字段的挖掘结构。 最后，创建一个针对特定的客户属性（如 Region）进行筛选的模型。 随后，您即可以方便地创建该模型的副本，而且只需更改筛选条件即可基于不同的区域生成新模型。  
  
 下面是一些可能受益于此功能的现实情况：  
  
-   为离散值（如性别、区域等）创建单独的模型。 例如，服装店可以使用客户统计数据来按性别生成不同的模型，即使所有客户的销售数据来自同一个数据源也是如此。  
  
-   通过创建并测试相同数据的不同分组（如年龄段 20-30 、年龄段 20-40 和年龄段 20-25）来试验模型。  
  
-   针对嵌套表内容指定复杂的筛选器，例如，要求只有当客户至少购买了两件特定商品时才在模型中包括一个事例。  
  
 本节介绍如何针对挖掘模型生成、使用和管理筛选器。  
  
## <a name="creating-model-filters"></a>创建模型筛选器  
 可以按如下方式创建和应用筛选器：  
  
-   使用数据挖掘设计器中的 **“挖掘模型”** 选项卡，并借助筛选器编辑器对话框生成各个条件。  
  
-   在挖掘模型的 **“筛选器”** 属性中直接键入筛选表达式。  
  
-   使用 AMO 以编程方式对模型设置筛选条件。  
  
### <a name="creating-model-filters-using-data-mining-designer"></a>使用数据挖掘设计器创建模型筛选器  
 可以通过更改挖掘模型的 **Filter** 属性在数据挖掘设计器中筛选模型。 可以在 **“属性”** 窗格中直接键入筛选表达式，也可以打开一个筛选器对话框来生成条件。  
  
 共有两个筛选器对话框。 第一个对话框可用来创建应用于事例表的条件。 如果数据源中包含多个表，请首先选择一个表，然后选择一列并指定应用于该列的运算符和条件。 可使用 **AND**/**OR** 运算符链接多个条件。 可用于定义值的运算符取决于该列是包含离散值还是连续值。 例如，对于连续值，可以使用 **greater than** 和 **less than** 运算符。 但是，对于离散值，则仅可使用 **=（等于）**、 **!=（不等于）**和 **is null** 运算符。  
  
> [!NOTE]  
>  不支持使用 **LIKE** 关键字。 如果您希望包括多个离散属性，则必须创建不同条件并使用 **OR** 运算符来链接它们。  
  
 如果条件非常复杂，则可以使用第二个筛选器对话框，一次处理一个表。 当您关闭第二个筛选器对话框时，系统会对筛选表达式进行求值，并将值与对事例表中其他列设置的筛选条件合并。  
  
### <a name="creating-filters-on-nested-tables"></a>针对嵌套表创建筛选器  
 如果数据源视图中包含嵌套表，则可以使用第二个筛选器对话框来针对嵌套表中的行生成条件。  
  
 例如，如果您的事例表与客户相关，而且嵌套表中显示客户已经购买的产品，则可以通过在嵌套表的筛选器中使用下面的语法来为已经购买了特定商品的客户创建一个筛选器： `[ProductName]=’Water Bottle’ OR ProductName=’Water Bottle Cage'`。  
  
 还可以使用 **EXISTS** 或 **NOT EXISTS** 关键字和子查询在嵌套表中筛选特定值，以查看其是否存在。 这允许您创建诸如 `EXISTS (SELECT * FROM Products WHERE ProductName=’Water Bottle’)`之类的条件。 如果嵌套表中至少有一行包括 `EXISTS SELECT(<subquery>)` 值，则 **将返回** true `Water Bottle`。  
  
 可以将事例表中的条件与嵌套表中的条件组合起来。 例如，下面的语法包括事例表中的一个条件 (`Age > 30` )、嵌套表中的一个子查询 (`EXISTS (SELECT * FROM Products)`) 以及嵌套表中的多个条件 (`WHERE ProductName=’Milk’  AND Quantity>2`)。  
  
```  
(Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’  AND Quantity>2) )  
```  
  
 在完成筛选器的生成之后，筛选器文本将由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]进行求值，转换为 DMX 表达式，之后将随模型一起保存。  
  
 有关如何在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中使用筛选器对话框的说明，请参阅 [对挖掘模型应用筛选器](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md)。  
  
## <a name="managing-mining-model-filters"></a>管理挖掘模型筛选器  
 基于数据的模型筛选大大简化了管理挖掘结构和挖掘模型的任务，因为您可以基于同一个结构方便地创建多个模型。 您还可以快速创建现有挖掘模型的多个副本，之后将只需更改筛选条件。 但是，筛选器会导致某些混淆。  
  
 以下是有关如何管理和解释有关挖掘模型的筛选器的常见问题：  
  
### <a name="how-can-i-tell-whether-a-filter-is-being-used"></a>我如何分辨是否正在使用筛选器？  
 可以使用多种方法确定是否对模型应用了筛选器：  
  
-   在设计器中，单击 **“挖掘模型”** 选项卡，打开 **“属性”**，然后查看挖掘模型的 **Filter** 属性。  
  
-   DMV DMSCHEMA_MINING_MODELS 将输出一个包含筛选器文本的列。 您可以使用以下有关 DMV 的查询来返回模型的名称及其筛选器：  
  
    ```  
    SELECT MODEL_NAME, [FILTER]   
    FROM $SYSTEM.DMSCHEMA_MINING_MODELS  
  
    ```  
  
-   您可以在 AMO 中获取 MiningModel 对象的 Filter 属性的值，或在 XMLA 中检查 Filter 元素。  
  
 您还可以建立模型的命名约定以反映筛选器的内容。 这样可更易于分辨相关模型。  
  
### <a name="how-can-i-save-a-filter"></a>如何保存筛选器？  
 筛选表达式将保存为脚本，并随其关联挖掘模型或嵌套表一起存储。 如果删除了筛选器文本，则只能通过手动重新创建筛选表达式的方式来将其还原。 因此，如果创建了复杂的筛选表达式，还应当创建筛选器文本的备份副本。  
  
### <a name="why-cant-i-see-any-effects-from-the-filter"></a>为什么从筛选器中看不到任何效果？  
 无论何时更改或添加筛选表达式，都必须重新处理挖掘结构和挖掘模型，然后才能查看筛选器的效果。  
  
### <a name="why-do-i-see-filtered-attributes-in-prediction-query-results"></a>为什么我在预测查询结果中会看到已筛选的属性？  
 对模型应用筛选器时，仅影响对用于培训模型的事例的选择。 筛选器不会影响对模型已知的属性，或更改或取消显示数据源中显示的数据。 因此，针对模型的查询可以返回对其他事例类型的预测，且模型使用的值的下拉列表可能会显示筛选器所排除的属性值。  
  
 例如，假设您培训仅使用涉及 20-30 年龄段的女性的事例的 [自行车购买者] 模型。 您仍可以运行预测某个男性购买自行车的可能性的预测查询，或者预测 30-40 年龄段的女性的购买结果。 这是因为数据源中显示的属性和值定义理论上的可能性，而事例定义用于培训的实际发生情况。 但是，这些查询将返回非常小的可能性，因为培训数据不包含任何带有目标值的事例。  
  
 如果您需要在模型中完全隐藏或匿名属性值，可采取几个不同的方法：  
  
-   筛选作为数据源视图定义的一部分或在关系数据源中的传入数据。  
  
-   对属性值进行掩码或编码。  
  
-   将已排除的值作为挖掘结构定义的一部分折叠到某个类别中。  
  
## <a name="related-resources"></a>相关资源  
 有关筛选器语法和筛选器表达式示例的详细信息，请参阅 [模型筛选器语法和示例（Analysis Services – 数据挖掘）](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)。  
  
 有关在测试挖掘模型时如何使用模型筛选器的信息，请参阅 [选择准确性图表类型和设置图表选项](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)。  
  
## <a name="see-also"></a>另请参阅  
 [模型筛选器语法和示例（Analysis Services – 数据挖掘）](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [测试和验证（数据挖掘）](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
