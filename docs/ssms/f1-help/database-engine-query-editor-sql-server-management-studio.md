---
title: 数据库引擎查询编辑器
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.tsqlquery.f1
dev_langs:
- TSQL
helpviewer_keywords:
- Query Editor [Database Engine]
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Query Editor [Database Engine], Toolbar
- editors [SQL Server Management Studio], Database Engine Query Editor
- Query Editor [Database Engine], Features
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/03/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 685397689b390175bd15f6241fc7036004e1e97a
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2020
ms.locfileid: "79198524"
---
# <a name="ssms-query-editor"></a>SSMS 查询编辑器

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

数据库引擎查询编辑器是在 SQL Server Management Studio (SSMS) 中实现的四个编辑器之一。

使用查询编辑器创建和运行包含 Transact-SQL 语句的脚本。 此编辑器还支持包含 **sqlcmd** 命令的正在运行的脚本。

对于在查询编辑器中实现的功能以及使用此编辑器可以执行的主要任务的说明，请参阅[查询和文本编辑器](../scripting/query-and-text-editors-sql-server-management-studio.md)

![新建查询](media/database-engine-query-editor-sql-server-management-studio/new-query.png)

## <a name="transact-sql-f1-help"></a>Transact-SQL F1 帮助

查询编辑器支持在你选中 F1 时将你链接到特定 Transact-SQL 语句的参考主题。 为此，突出显示 Transact-SQL 语句的名称，然后选择 F1。 接着，帮助搜索引擎将搜索具有与突出显示的字符串匹配的 F1 帮助属性的主题。

如果帮助搜索引擎找不到具有与突出显示的字符串完全匹配的 F1 帮助关键字的主题，则无法显示该主题。 在这种情况下，有两种方法可以找到所需的帮助：

- 将您突出显示的编辑器字符串复制并粘贴到 SQL Server 联机丛书的搜索选项卡中，并执行搜索。

- 仅突出显示 Transact-SQL 语句中可能与应用于主题的 F 帮助关键字匹配的部分，然后再次选择 F1。 搜索引擎要求突出显示的字符串与分配给主题的 F1 帮助关键字之间完全匹配。 如果突出显示的字符串包含对于您的环境是唯一的元素（如列或参数名称），则搜索引擎不会获得匹配项。 要突出显示的字符串的示例包括：

  - Transact-SQL 语句的名称，如 SELECT、CREATE DATABASE 或 BEGIN TRANSACTION。

  - 内置函数的名称，如 SERVERPROPERTY 或 @@VERSION。

  - 系统存储过程表或视图的名称，如 sys.data_spaces 或 sp_tableoption。

## <a name="sql-editor-toolbar"></a>SQL 编辑器工具栏

查询编辑器打开时，SQL 编辑器工具栏上显示以下按钮。

通过依次选择 **“视图”** 菜单、 **“工具栏”** 和 **“SQL 编辑器”** ，还可添加 SQL 编辑器工具栏。 如果在没有打开任何查询编辑器窗口时添加 SQL 编辑器工具栏，则所有按钮都不可用。

![编辑器工具栏](media/database-engine-query-editor-sql-server-management-studio/editor-toolbar.png)

### <a name="connect-using-the-editor-toolbar"></a>使用编辑器工具栏连接

打开[“连接到服务器”](connect-to-server-database-engine.md)  对话框。 此对话框用于建立与服务器的连接。

还可以使用[上下文菜单](#connection-using-the-context-menu)连接到数据库。

### <a name="change-connection-using-the-editor-toolbar"></a>使用编辑器工具栏更改连接

打开“连接到服务器”  对话框。 使用对话框建立[与另一个服务器的连接](f1-help-for-server-connections-sql-server-management-studio.md)。

还可以使用[上下文菜单](#connection-using-the-context-menu)更改连接。

### <a name="available-databases-using-the-editor-toolbar"></a>使用编辑器工具栏的可用数据库

将连接更改到同一服务器上的其他数据库。

### <a name="execute-using-the-editor-toolbar"></a>使用编辑器工具栏执行

执行所选的代码，如果没有选择任何代码，则执行查询编辑器中的全部代码。

还可以通过选中 F5 或从[上下文菜单](#execute-using-the-context-menu)“执行”  查询。

### <a name="cancel-executing-query-using-the-editor-toolbar"></a>使用编辑器工具栏取消执行查询

向服务器发送取消请求。 有些查询不能立即取消，而必须等待适当的取消条件。 取消事务时，在回滚事务期间可能发生延迟。

还可以通过选中 Alt + Break 来取消正在执行的查询。

### <a name="parse-using-the-editor-toolbar"></a>使用编辑器工具栏进行分析

检查所选代码的语法。 如果没有选择任何代码，则检查查询编辑器窗口中全部代码的语法。

还可以通过选中 Ctrl + F5 在查询编辑器中检查代码。

### <a name="display-estimated-execution-plan-using-the-editor-toolbar"></a>使用编辑器工具栏显示估计的执行计划

从查询处理器中请求查询执行计划而不实际执行查询，并在“执行计划”  窗口中显示该计划。 此计划使用索引统计值作为查询执行的各个部分预期返回的行数估计值。 实际使用的查询计划可能与估计的执行计划不同。 如果返回的行数与估计值有明显差距，并且查询处理器更改了执行计划以提高其效率，就会发生这种情况。

还可以通过选中 Ctrl + L 或从[上下文菜单](#display-estimated-execution-plan-using-the-context-menu)显示估计的执行计划。

### <a name="query-options-using-the-editor-toolbar"></a>使用编辑器工具栏的“查询选项”

打开“查询选项”  对话框。 此对话框用于配置查询执行和查询结果的默认选项。

还可以从[上下文菜单](#query-options-using-the-context-menu)中选择“查询选项”  。

### <a name="intellisense-enabled-using-the-editor-toolbar"></a>使用编辑器工具栏启用 IntelliSense

指定 IntelliSense 功能在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器中是否可用。 默认情况下设置此选项。

还可以通过选中 Ctrl + B 然后按 Ctrl I，或从[上下文菜单](#intellisense-enabled-using-the-context-menu)中选择“IntelliSense 已启用”  。

### <a name="include-actual-execution-plan-using-the-editor-toolbar"></a>使用编辑器工具栏包括实际执行计划

执行查询，返回查询结果和用于查询的执行计划。 这些内容在 **“执行计划”** 窗口中显示为图形查询计划。

还可以通过选中 Ctrl + M 或从[上下文菜单](#include-actual-execution-plan-using-the-context-menu)选择“包括实际执行计划”  。

### <a name="include-live-query-statistics-using-the-editor-toolbar"></a>使用编辑器工具栏包括实时查询统计信息

作为控制流，能够实时了解从一个查询计划操作员到另一个操作员的查询执行过程。

还可以从[上下文菜单](#include-live-query-statistics-using-the-context-menu)选择“包括实时查询统计信息”  。

### <a name="include-client-statistics-using-the-editor-toolbar"></a>使用编辑器工具栏包括客户端统计信息

提供一个“客户端统计信息”  窗口，其中包含有关查询、网络数据包以及查询占用时间的统计信息。

还可以通过选中 Shift + Alt + S 或从[上下文菜单](#include-client-statistics-using-the-context-menu)选择“包括实时查询统计信息”  。

### <a name="results-to-text-using-the-editor-toolbar"></a>使用编辑器工具栏将结果显示为文本

在“结果”  窗口中以文本格式返回查询结果。

还可以通过选中 Ctrl + T 或从[上下文菜单](#results-using-the-context-menu)返回将结果显示为文本。

### <a name="results-to-grid-using-the-editor-toolbar"></a>使用编辑器工具栏将结果显示为网格

在“结果”  窗口中以一个或多个网格的形式返回查询结果。 此选项在默认情况下通常启用。

还可以通过选中 Ctrl + D 或从[上下文菜单](#results-using-the-context-menu)返回将结果显示为文本。

### <a name="results-to-file-using-the-editor-toolbar"></a>使用编辑器工具栏将结果显示为文件

在执行查询时，“保存结果”  对话框将会打开。 在 **“保存于”** 中，选择要将文件保存到的文件夹。 在“文件名”  中键入文件的名称，然后选择“保存”  将查询结果保存为具有 .rpt 扩展名的“报表”  文件。 对于高级选项，请单击“保存”  按钮上的向下箭头，再选择“编码保存”  。

还可以通过选中 Ctrl + Shift + F 或从[上下文菜单](#results-using-the-context-menu)返回将结果显示为文本。

### <a name="comment-out-the-selected-lines-using-the-editor-toolbar"></a>使用编辑器工具栏注释掉所选行

在当前行的开头处添加一个注释运算符 (--)，以对该行进行注释。

还可以通过选中 Ctrl + K 然后选择 Ctrl + C 注释掉一行。

### <a name="uncomment-the-selected-lines-using-the-editor-toolbar"></a>使用编辑器工具栏取消注释所选行

删除当前行开头处的任何注释运算符 (--)，以使该行成为一个活动的源语句。

还可以通过选择 Ctrl + K 然后选择 Ctrl + U 来取消对某行的注释。

### <a name="decrease-indent-using-the-editor-toolbar"></a>使用编辑器工具栏减少缩进

删除行开头处的空格，从而使该行文本向左移动。

### <a name="increase-line-indent-using-the-editor-toolbar"></a>使用编辑器工具栏增加行缩进

在行开头处插入空格，从而使该行文本向右移动。

### <a name="specify-values-for-template-parameters-using-the-editor-toolbar"></a>使用编辑器工具栏指定模板参数的值

打开一个对话框，在此对话框中可以指定存储过程或函数中参数的值。

## <a name="context-menu"></a>上下文菜单

可以通过在查询编辑器的任意位置右键单击来访问上下文菜单  。 上下文菜单中的选项类似于 SQL 编辑器工具栏。 在上下文菜单中，可以看到诸如“连接”  和“执行”  的相同选项，但也可以看到列出的其他选项，例如“插入代码片段”  和“外侧代码”  。

![上下文菜单选项](media/database-engine-query-editor-sql-server-management-studio/context-menu.png)

### <a name="insert-snippet-using-the-context-menu"></a>使用上下文菜单插入代码片段

Transact-SQL 代码片段是一个模板，可将其作为在查询编辑器中编写新 Transact-SQL 语句的起点。

### <a name="surround-with-using-the-context-menu"></a>使用上下文菜单的外侧代码

外侧代码片段是一个模板，可将其作为在 BEGIN、IF 或 WHILE 块中插入一组 Transact-SQL 语句的起点。

### <a name="connection-using-the-context-menu"></a>使用上下文菜单的“连接”

![上下文菜单选项](media/database-engine-query-editor-sql-server-management-studio/context-menu-connections.png)

与 SSMS 中的工具栏选项相比，上下文菜单中的“连接”  选项更多。

- **连接** - 打开“连接到服务器”对话框。 此对话框用于建立与服务器的连接。

- **断开连接** - 断开当前查询编辑器与服务器的连接。

- **断开所有查询** - 断开所有查询连接。

- **更改连接** - 打开“连接到服务器”对话框。 此对话框用于建立与另一个服务器的连接。

### <a name="open-server-in-object-explorer-using-the-context-menu"></a>使用上下文菜单在对象资源管理器中打开服务器

对象资源管理器提供一个层次结构用户界面，用于查看和管理每个 SQL Server 实例中的对象。 “对象资源管理器详细信息”窗格显示一个实例对象的表格视图以及用于搜索特定对象的功能。 对象资源管理器的功能根据服务器的类型稍有不同，但一般都包括用于数据库的开发功能和用于所有服务器类型的管理功能。

### <a name="execute-using-the-context-menu"></a>使用上下文菜单执行

执行所选的代码，如果没有选择任何代码，则执行查询编辑器中的全部代码。

### <a name="display-estimated-execution-plan-using-the-context-menu"></a>使用上下文菜单显示估计的执行计划

从查询处理器中请求查询执行计划而不实际执行查询，并在“执行计划”  窗口中显示该计划。 此计划使用索引统计值作为查询执行的各个部分预期返回的行数估计值。 实际使用的查询计划可能与估计的执行计划不同。 如果返回的行数与估计值有明显差距，并且查询处理器更改了执行计划以提高其效率，就会发生这种情况。

### <a name="intellisense-enabled-using-the-context-menu"></a>使用上下文菜单启用 IntelliSense

指定 IntelliSense 功能在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器中是否可用。 默认情况下设置此选项。

### <a name="trace-query-in-sql-server-profiler-using-the-context-menu"></a>使用上下文菜单在 SQL Server Profiler 中进行跟踪查询

SQL Server Profiler 是一个界面，用于创建和管理跟踪并分析和重播跟踪结果。 这些事件保存在一个跟踪文件中，稍后试图诊断问题时，可以对该文件进行分析或用它来重播一系列特定的步骤。

### <a name="analyze-query-in-database-engine-tuning-advisor-using-the-context-menu"></a>使用上下文菜单在数据库引擎优化顾问中分析查询

Microsoft 数据库引擎优化顾问 (DTA) 分析数据库并对优化查询性能提出建议。 借助数据库引擎优化顾问，你不必精通数据库结构或深谙 SQL Server，即可选择和创建索引、索引视图和分区的最佳集合。 使用 DTA，您可以执行以下任务。

### <a name="design-query-in-editor-using-the-context-menu"></a>使用上下文菜单在编辑器中设计查询

当您打开视图的定义、显示查询或视图的结果或者创建或打开查询时，查询和视图设计器将会打开。

### <a name="include-actual-execution-plan-using-the-context-menu"></a>使用上下文菜单包括实际执行计划

执行查询，返回查询结果和用于查询的执行计划。 这些内容在 **“执行计划”** 窗口中显示为图形查询计划。

### <a name="include-live-query-statistics-using-the-context-menu"></a>使用上下文菜单包括实时查询统计信息

作为控制流，能够实时了解从一个查询计划操作员到另一个操作员的查询执行过程。

### <a name="include-client-statistics-using-the-context-menu"></a>使用上下文菜单包括客户端统计信息

提供一个“客户端统计信息”  窗口，其中包含有关查询、网络数据包以及查询占用时间的统计信息。

### <a name="results-using-the-context-menu"></a>使用上下文菜单的“结果”

![“结果”选项](media/database-engine-query-editor-sql-server-management-studio/context-menu-results.png)

可以从上下文菜单中选择所需的任一“结果”  选项。

- **结果显示为文本** - 在“结果”  窗口中将查询结果返回为文本。

- **结果显示为网格** - 在“结果”  窗口中将查询结果返回为一个或多个网格。

- **结果显示为文件** - 在执行查询时，  “保存结果”对话框将会打开。 在 **“保存于”** 中，选择要将文件保存到的文件夹。 在“文件名”  中键入文件的名称，然后选择“保存”  将查询结果保存为具有 .rpt 扩展名的“报表”  文件。 对于高级选项，请单击“保存”  按钮上的向下箭头，再选择“编码保存”  。

### <a name="properties-window-using-the-context-menu"></a>使用上下文菜单的“属性”窗口

[“属性”窗口](../menu-help/properties-window-f1-help-management-studio.md)说明 SQL Server Management Studio 中项（如连接或 Showplan 运算符）的状态，以及有关数据库对象（如表、视图和设计器等）的信息。

可以使用“属性”窗口查看当前连接的属性。 许多属性在“属性”窗口中是只读的，但可以在 Management Studio 的其他地方更改。 例如，查询的数据库属性在“属性”窗口中是只读的，但可在工具栏上更改。

### <a name="query-options-using-the-context-menu"></a>使用上下文菜单的“查询选项”

打开“查询选项”  对话框。 此对话框用于配置查询执行和查询结果的默认选项。

## <a name="see-also"></a>另请参阅

- [自定义菜单和快捷键](../customize-menus-and-shortcut-keys.md)

- [SQL Server Management Studio 备选项](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)
