---
title: "使用“结果”窗格中的数据 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- View Designer, Results pane
- queries [Visual Database Tools]
- result sets [SQL Server], queries
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- Visual Database Tools [SQL Server], queries
- queries [SQL Server], results
- Results pane
ms.assetid: 4f8a0080-91ef-4442-83ae-53be2f478c54
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 43805e99f16d522e7b9a82e1af4514ad3c8fa043
ms.lasthandoff: 04/11/2017

---
# <a name="work-with-data-in-the-results-pane-visual-database-tools"></a>使用“结果”窗格中的数据 (Visual Database Tools)
在运行查询或视图之后，将在“结果”窗格中显示结果。 然后您就可以对这些结果进行处理。 例如，您可以添加和删除行、输入或更改数据以及在大型结果集中轻松导航。  
  
以下信息可以帮助您避免问题并提高处理结果集的效率：  
  
## <a name="returning-the-results-set"></a>返回结果集  
您可以从查询或视图返回结果，并且可以选择是仅打开“结果”窗格还是打开所有窗格。 在这两种情况下，都会在查询和视图设计器中打开该查询或视图。 两者之间的区别是：一个打开时仅显示“结果”窗格，另一个打开时则显示“选项”对话框中选择的所有窗口。 默认为所有四个窗格（“结果”、SQL、“关系图”和“条件”）。  
  
有关详细信息，请参阅[打开查询 (Visual Database Tools)](../../ssms/visual-db-tools/open-queries-visual-database-tools.md)。  
  
若要更改查询或视图的设计，以使其返回不同的结果集或以不同的顺序返回记录，请参阅[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md) 中所列的主题。  
  
您还可以通过以下两种方式来决定是返回全部结果集还是返回部分结果集：在查询运行时停止查询或在查询运行前选择返回的结果数量。  
  
## <a name="navigating-in-the-results-pane"></a>在“结果”窗格中导航  
您可以使用“结果”窗格底部的导航栏在记录之间快速导航。  
  
导航栏中提供了多个按钮，可分别用于跳转到第一个记录、最后一个记录、下一个记录、上一个记录以及某个特定记录。  
  
若要转到特定的记录，请在导航栏的文本框中键入行号，然后按 Enter。  
  
有关在查询和视图设计器中使用键盘快捷方式的信息，请参阅[在查询和视图设计器中导航 (Visual Database Tools)](../../ssms/visual-db-tools/navigate-in-the-query-and-view-designer-visual-database-tools.md)。  
  
## <a name="committing-changes-to-the-database"></a>将更改提交到数据库  
“结果”窗格使用开放式并发控制，因此该网格显示的是数据库中数据的副本而不是完全实时的视图。 这样，只有当您离开行时，才会将更改提交给数据库。 这允许一个以上的用户同时使用数据库。 如果存在冲突（例如，如果另一个用户更改了您更改的相同的行，并在您提交前将其提交给了数据库），您将收到一条消息，告诉您该冲突并提供解决方案。  
  
## <a name="undo-changes-using-esc"></a>使用 Esc 撤消更改  
只有在更改尚未提交到数据库时，才能撤消更改。 如果您尚未离开记录或者当离开记录时收到错误信息，指出无法提交该更改，则不会提交数据。 如果尚未提交更改，则可以使用 Esc 键来撤消更改。  
  
若要撤消对某一行的所有更改，请移动到该行中尚未编辑过的单元格，然后按 Esc 键。  
  
若要撤消对已编辑的特定单元格的更改，请移动到该单元格，然后按 Esc 键。  
  
## <a name="adding-or-deleting-data-in-the-database"></a>在数据库中添加或删除数据  
为了了解数据库设计的工作情况，可能需要向数据库中添加示例数据。 您可以直接向“结果”窗格中输入示例数据，也可以从其他程序（如“记事本”或 Excel）复制示例数据，然后将其粘贴到“结果”窗格中。  
  
除了可以向“结果”窗格中复制行之外，您还可以添加新记录或者修改或删除现有记录。 有关详细信息，请参阅[在“结果”窗格中添加新行 (Visual Database Tools)](../../ssms/visual-db-tools/add-new-rows-in-the-results-pane-visual-database-tools.md)、[在“结果”窗格中删除行 (Visual Database Tools)](../../ssms/visual-db-tools/delete-rows-in-the-results-pane-visual-database-tools.md) 和[在“结果”窗格中编辑行 (Visual Database Tools)](../../ssms/visual-db-tools/edit-rows-in-the-results-pane-visual-database-tools.md)。  
  
## <a name="tips-for-working-with-null-values-and-empty-cells"></a>关于处理 NULL 值和空单元格的提示  
单击一个空行以添加新记录时，所有列的初始值均为 NULL。 如果列允许空值，则可将保留空值。  
  
若要使用空值替换非空值，请键入大写字母的 NULL。 “结果”窗格将对该词应用倾斜格式，以表示它将被识别为空值而不是字符串。  
  
若要键入字符串“null”，请键入这些字母（不包括引号）。 只要有一个字母是小写字母，该值就会被视为字符串而不是空值。  
  
对于数据类型为 binary 的列，默认情况下其值为 NULL。 这些值不能在“结果”窗格中进行更改。  
  
若要输入空格而不是使用空值，请删除现有的文本并离开该单元格。  
  
## <a name="validating-data"></a>验证数据  
查询和视图设计器可以根据列属性来验证某些类型的数据。 例如，如果您在数据类型为 float 的列中输入“abc”，您将收到错误，并且该更改不会提交到数据库。  
  
在“结果”窗格中，查看列的数据类型的最快捷的方法是：打开“关系图”窗格并悬停在表或表值对象中列的名称上。  
  
> [!NOTE]  
> “结果”窗格可以为 text 数据类型显示的最大长度为 2,147,483,647。  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>使结果集与查询定义保持同步  
当您处理查询或视图的结果时，可能会出现“结果”窗格中的记录与查询定义不同步的情况。 例如，如果您用查询搜索出表的五列中的四列，然后使用“关系图”窗格将第五列添加到查询的定义中，则第五列的数据不会自动添加到“结果”窗格中。 若要使“结果”窗格反映新的查询定义，请再次运行该查询。  
  
您可以这样来判断：“结果”窗格的右下角出现一个警报图标和文本“查询已更改”，并且该图标在窗格的左上角反复出现。  
  
## <a name="reconciling-changes-made-by-multiple-users"></a>协调多个用户所做的更改  
在处理查询或视图的结果时，所处理的记录可能会被另一个也在处理数据库的用户所更改。  
  
如果出现此情况，当您离开发生冲突的单元格时，将会立即收到通知。 然后您可以重写其他用户的更改，用其他用户的更改更新您的“结果”窗格或者仍然编辑您的“结果”窗格而不协调差异。 如果选择不协调差异，则不会将您所做的更改提交到数据库。  
  
## <a name="limitations-in-the-results-pane"></a>“结果”窗格中的限制  
  
### <a name="what-can-not-be-updated"></a>不能更新的内容  
以下提示可能有助于您成功地处理“结果”窗格中的数据。  
  
-   如果查询中包括的列来自多个表或视图，则不能更新该查询。  
  
-   只有当数据库约束允许更新视图时，才能更新视图。  
  
-   不能更新存储过程返回的结果。  
  
-   不能更新使用 GROUP BY、DISTINCT 或 TO XML 子句的查询或视图。  
  
-   表值函数返回的结果只有在某些情况下才能更新。  
  
-   由查询中的表达式生成的列中的数据。  
  
-   提供程序未成功转换的数据。  
  
### <a name="what-can-not-be-represented-fully"></a>不能完全呈现的内容  
从数据库返回“结果”窗格的内容很大程度上受您所使用的数据源的提供程序控制。 “结果”窗格并不总是能转换所有数据库管理系统中的数据。 在以下情况下便是如此。  
  
-   Binary 数据类型对于在“结果”窗格中执行操作的人来说通常没什么用处，并且可能需要很长时间才能下载。 因此它们由 <Binary data> 或 Null 表示。  
  
-   并不能始终保留精度和小数位数。 例如，结果窗格支持的精度为 27。 如果数据的数据类型的精度比这个值大，数据可能会截断或可能由 *<Unable to read data>*表示。  
  
## <a name="see-also"></a>另请参阅  
[执行基本的查询操作 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[指定搜索条件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

