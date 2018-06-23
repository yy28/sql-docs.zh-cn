---
title: 创建预测查询使用预测查询生成器 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- prediction queries [Analysis Services]
- Mining Model Prediction [Analysis Services], prediction queries
ms.assetid: e02836e5-dd8c-4c97-a078-840ae79d3660
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 947c188fcca3a1b08f335ca7fad476465aca2ddf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017857"
---
# <a name="create-a-prediction-query-using-the-prediction-query-builder"></a>使用预测查询生成器创建预测查询
  可在 BI Development Studio 中生成数据挖掘解决方案时创建预测查询，或在 SQL Server Management Studio 中右键单击现有挖掘模型，然后选择“生成预测查询”选项以创建预测查询。  
  
 “预测查询生成器”包含以下三种设计模式，可单击左上角的图标在这三种模式之间切换。  
  
-   **设计**  
  
-   **查询**  
  
-   **结果**  
  
 利用 **“设计”** 模式，您可生成预测查询，方式为选择输入数据，将数据映射到模型中，然后将预测函数添加到使用网格生成的语句中。 设计网格包含以下生成块：  
  
 **数据源**  
 选择新列的源。 您可使用挖掘模型中的列、数据源视图中包含的输入表、预测函数或自定义表达式。  
  
 **字段**  
 确定与“源”列中的选择相关联的特定列或函数。  
  
 **别名**  
 确定如何在结果集中命名列。  
  
 **显示**  
 确定在“源”列中选择的内容是否显示在结果中。  
  
 **分组**  
 通过使用括号来与“和/或”列一起使用以便将表达式组合到一起。 例如，(expr1 or expr2) and expr3。  
  
 **和/或**  
 在查询中创建逻辑。 例如，(expr1 or expr2) and expr3。  
  
 **条件/参数**  
 指定应用于该列的条件或用户表达式。 您可以将列从表拖至该单元格。  
  
 “查询”模式提供了一个可用于直接访问数据挖掘扩展插件 (DMX) 语言的文本编辑器，以及一个输入数据和模型列的视图。 选择 **“查询”** 模式时，一个基本文本编辑器将替换用于定义查询的网格。 您可使用此编辑器复制并保存编写的查询，或从剪贴板将其粘贴到现有 DMX 查询中，然后运行它们。  
  
 **“结果”** 视图运行当前查询，并将结果显示在网格中。 如果基础数据已更改，并且要重新运行该查询，请单击状态栏的“开始”按钮。  
  
 可结合使用可视工具和文本编辑器来设计数据挖掘查询。 如果在文本编辑器中键入对查询的更改，并切换回 **“设计”** 视图，则所有更改都将丢失，查询将恢复到预测查询生成器所创建的原始查询。本主题指导您使用图形查询生成器。  
  
### <a name="to-create-a-prediction-query"></a>创建预测查询  
  
1.  在数据挖掘设计器中，单击 **“挖掘模型预测”** 选项卡。  
  
2.  在 **“挖掘模型”** 表中，单击 **“选择模型”** 。  
  
     此时将打开 **“选择挖掘模型”** 对话框，以显示当前项目中存在的所有挖掘结构。  
  
3.  选择要为其创建预测的模型，再单击 **“确定”**。  
  
4.  在“选择输入表”表上，单击“选择事例表”。  
  
     将打开 **“选择表”** 对话框。  
  
5.  在 **“数据源”** 列表中选择数据源，该数据源应当包含创建预测所基于的数据。  
  
6.  在“表/视图名称”框中选择包含创建预测所基于的数据的表，然后单击“确定”。  
  
     选择输入表之后，预测查询生成器便会根据各列的名称在挖掘模型和输入表之间创建默认映射。 若要删除映射，请单击以选择相应的行（该行将“挖掘模型”表中的列链接到“选择输入表”表中的被映射列），再按 Delete 键。 也可以手动创建映射，方法是单击“选择输入表”表中的列，然后将其拖到“挖掘模型”表中对应的列上。  
  
7.  将以下三种类型的信息的任意组合添加到预测查询生成器网格中：  
  
    -   **“挖掘模型”** 框中的可预测列。  
  
    -   “选择输入表”框中的输入列的任意组合。  
  
    -   预测函数  
  
8.  单击 **“挖掘模型预测”** 选项卡的工具栏上的第一个按钮，以运行查询，再选择 **“结果”**。  
  
## <a name="see-also"></a>请参阅  
 [在数据挖掘设计器中创建单独查询](create-a-singleton-query-in-the-data-mining-designer.md)   
 [数据挖掘查询](data-mining-queries.md)  
  
  