---
title: 将列添加到表 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5974a3cc-caf8-4558-8836-6e3c24b1ee23
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12534cd4554d71c368f09a6620056e187578b456
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326507"
---
# <a name="add-columns-to-a-table-ssas-tabular"></a>将列添加到表（SSAS 表格）
  本主题介绍如何向现有表中添加列。  
  
## <a name="add-columns-from-the-data-source"></a>从数据源添加列  
 使用表导入向导从数据源表导入数据时，将在模型中创建一个新表，该表包含源表中的所有列，如果您选择使用“预览并筛选”功能来筛选出某些列，则仅包含您选择的那些列和已筛选数据。 您还可以编写一个指定要导入的那些列的 SQL 查询。 但是，您可能以后决定源表具有要添加到模型表的其他列，或需要添加其值从 DAX 公式派生的计算列。  
  
 例如，如果在您最初从数据源导入时使用了表导入向导的“预览并筛选”功能以从源表选择有限数目的列，以后又决定添加在源表中存在而在模型表中不存在的另一个列。 或者，例如，在数据源将新的 AdjustedProfit 列添加到 FactSales 表，现在要向模型中的 Sales 表添加同样的 AdjustedProfit 列和数据。  
  
 在这些情况下，您可以使用“编辑表属性”对话框来从源表选择列并将它们添加到模型表。 “编辑表属性”对话框包含表预览窗口。 表预览窗口显示源中的表。 已包含在模型表定义中的列已被选中。 未包含在模型表定义中的那些列未被选中。 您可以通过选择列并单击“确定”，将源中的列添加到模型表定义。 “编辑表属性”对话框中的表预览窗口提供的视图和功能与表导入向导的“预览并筛选”页中表预览窗口提供的视图和功能相同。  
  
> [!IMPORTANT]  
>  将列添加到包含两个或更多分区的表时，在使用“编辑表属性”对话框将该列添加到表定义前，必须首先使用分区管理器将该列添加到所有定义的分区。 将该列添加到定义的分区后，可以使用“编辑表属性”对话框将相同的列添加到表定义中。  
  
> [!NOTE]  
>  如果在最初使用表导入向导导入数据时使用了 SQL 查询来选择表和列，必须在“编辑表属性”对话框中再次使用 SQL 查询来将这些列添加到模型表。  
  
#### <a name="to-add-a-column-from-the-data-source-by-using-the-edit-table-properties-dialog-box"></a>使用“编辑表属性”对话框从数据源添加列  
  
1.  在模型设计器中，单击要将列添加到的表，单击 **“表”** 菜单，然后单击  **“表属性”**。  
  
2.  在 **“编辑表属性”** 对话框中，在表预览窗口中选择要添加的源列，然后单击“确定”。 已包含在表定义中的列将被选中。  
  
## <a name="add-a-calculated-column"></a>添加计算列  
 在计算列中，DAX 公式用于定义每一行的值。 例如，您可以创建一个计算列，该列包含简单的公式 (=1) 以将值 1 添加到每行。 计算列还可以有更复杂的公式，以基于模型中的其他数据计算值。 将在其他主题中更详细介绍计算列。 有关详细信息，请参阅[计算列（SSAS 表格）](ssas-calculated-columns.md)。  
  
#### <a name="to-create-a-calculated-column"></a>创建计算列  
  
1.  在模型设计器的“数据视图”中，选择要添加新的空白计算列的表，滚动到最右侧的列，或单击“列”菜单，然后单击“添加列”。  
  
     若要在两个现有列之间创建新列，请右键单击某个现有列，然后单击“插入列”。  
  
2.  在公式栏中，键入 DAX 公式以便为每个行添加属性。  
  
## <a name="add-a-blank-column"></a>添加空白列  
 可以在模型表中创建命名的空白列。 如果要从另一个源粘贴数据，空白列很有用。 请记住，粘贴的数据的存储方式不同于导入的数据的存储方式。 有关详细信息，请参阅[复制并粘贴数据（SSAS 表格）](../copy-and-paste-data-ssas-tabular.md)。  
  
#### <a name="to-create-a-named-blank-column"></a>创建命名的空白列  
  
1.  在模型设计器的“数据视图”中，选择要添加空白列的表，滚动到最右侧的列，或单击“列”菜单，然后单击“添加列”。  
  
     若要在两个现有列之间创建新列，请右键单击某个现有列，然后单击“插入列”。  
  
2.  单击顶部的单元，然后键入名称，按 Enter。  
  
## <a name="see-also"></a>请参阅  
 [编辑表属性对话框&#40;SSAS&#41;](../edit-table-properties-dialog-box-ssas.md)   
 [更改表、 列或行筛选器映射&#40;SSAS 表格&#41;](change-table-column-or-row-filter-mappings-ssas-tabular.md)  
  
  
