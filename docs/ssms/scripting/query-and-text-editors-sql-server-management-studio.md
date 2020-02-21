---
title: 查询和文本编辑器 (SSMS)
description: 了解如何使用 SQL Server Management Studio (SSMS) 编辑器以交互方式查询、编辑和测试文件。
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio]
- Code Editor [SQL Server Management Studio], about Query Editor
- Query Editor [SQL Server Management Studio], full screen mode
- Query Editor [Database Engine], templates
- full screen mode [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], templates
- writing scripts
- modifying scripts
- SQL Server Management Studio [SQL Server], query editor
- Query Editor [SQL Server Management Studio], about Query Editor
- writing queries
- SQL Server Management Studio [SQL Server], editor
- scripts [SQL Server], SQL Server Management Studio
- queries [SQL Server], SQL Server Management Studio
ms.assetid: 062051e4-4b77-4969-98ae-d2547c24ce3e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 07ab012f916a86ca8642c81e2bdd87dfc815db2e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75558035"
---
# <a name="query-and-text-editors-sql-server-management-studio"></a>查询和文本编辑器 (SQL Server Management Studio)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  您可以使用任一 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 编辑器以交互方式编辑并测试 [!INCLUDE[tsql](../../includes/tsql-md.md)]、MDX、DMX 或 XML/A 脚本，或者编辑 XML 或纯文本文件。 每种编辑器都有特定于语言的服务提供的支持，该服务可以标出关键字颜色，并能检查语法和用法错误。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器包括一个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器，您可使用该调试器帮助修复 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码中的问题。  
  
## <a name="sql-server-management-studio-editors"></a>SQL Server Management Studio 编辑器

 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的四种编辑器共享共同的体系结构。 文本编辑器可实现基本功能，而且可用作文本文件的基本编辑器。 其他三个编辑器（或查询编辑器）可通过加入语言服务（用于定义 SQL Server 支持的其中一种语言的语法），对此基本功能进行扩展。 查询编辑器还可以对编辑器功能（如 IntelliSense 和调试）实现不同级别的支持。 查询编辑器包括用于生成包含 Transact-SQL 和 XQuery 语句的脚本的数据库引擎查询编辑器，用于 MDX 语言的 MDX 编辑器，用于 DMX 语言的 DMX 编辑器和用于 XML for Analysis 语言的 XML/A 编辑器。  
  
## <a name="common-components"></a>常见组件

 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的所有编辑器共享以下组件：  
  
 **代码窗格**  
 用于输入查询或文本的区域。 在查询编辑器中，此窗格包含各种对应于您所使用的语言的语句生成器功能。 文本编辑环境支持查找和替换、大量标注以及自定义字体和颜色。  
  
 由于该窗格与文本的缩进、跳格和拖放等操作相关，因此您可以在代码窗格中设置影响文本操作的选项。 可将查询窗口配置为以文档窗口中的选项卡形式或在单独的文档中进行操作。  
  
 **选定内容的边距**  
 位于边距指示符栏与代码文本之间的一列空白间距，单击该位置可选中文本行。 您可以隐藏或显示选定内容的边距。  
  
 **水平滚动条和垂直滚动条**  
 可让您水平或垂直地滚动代码窗格，以便查看超出代码窗格可视边缘的代码。  
  
 **行号**  
 用于在编辑器中的文本或代码的左侧显示行号。 您可以导航到特定行号。  
  
 **自动换行**  
 将较长的文本行或代码行以多行显示，以便您查看行中的所有内容。 在执行或打印文本时，自动换行选项不会影响文本的显示方式。 可以从 **“工具”** 、 **“选项”** 对话框（位于“文本编辑器”页、“所有语言”页、“常规”页或特定编辑器页上）中打开自动换行。  
  
## <a name="code-editor-components"></a>代码编辑器组件

 除了与文本和 XML 编辑器共享的功能之外，代码编辑器还包含以下功能：  
  
 **结果**  
 此窗口用于查看查询结果。 该窗口可以在网格或文本中显示结果，或者可将结果定向到某个文件。 结果网格能以单独的选项卡式窗口的形式显示。  
  
 **IntelliSense**  
 在编辑器的“编辑”  菜单上，指向“IntelliSense”  ，以查看 [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense 选项。  
  
 **颜色编码**  
 为每种类型的语法元素显示不同颜色，以提高复杂语句的可读性。  
  
 **代码大纲显示**  
 在代码左侧显示带有大纲显示线的代码组。 代码组可以折叠或展开，以方便查看代码。  
  
 **模板**  
 模板是包含创建数据库对象所需的语句基本结构的文件。 它们可以用于加快脚本编写速度。  
  
 **消息**  
 显示脚本运行时由服务器返回的错误、警告和信息性消息。 只有再次运行脚本时，消息列表才会发生变化。  
  
 **状态栏**  
 显示与查询编辑器窗口相关的系统信息，例如查询编辑器连接到哪个实例。  
  
## <a name="database-engine-query-editor-components"></a>数据库引擎查询编辑器组件

 以下组件仅在数据库引擎查询编辑器中提供：  
  
 **调试器**  
 可让您暂停执行特定语句的代码。 然后，您可以查看数据和系统信息，以帮助您找到代码中的错误。  
  
 **错误列表**  
 显示 IntelliSense 发现的语法和语义错误。 当您编辑 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本时，错误列表会动态变化。  
  
 **图形显示计划**  
 显示构成 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的执行计划的逻辑步骤。  
  
 **客户端统计信息**  
 显示有关划分为不同类别的查询执行的信息。 如果从 **“查询”** 菜单上选中 **“包括客户端统计信息”** ，则执行查询时将显示 **“客户端统计信息”** 窗口。 连续查询执行中的统计信息会与平均值一起列出。 从 **“查询”** 菜单上选择 **“重置客户端统计信息”** 可重置平均值。  
  
 **代码段**  
 当您在数据库引擎查询编辑器中添加语句时，可用作起点的模板。 您可以插入随 SQL Server 一起提供的预定义代码段，也可以添加您自己的代码段。  
  
 **SQLCMD 模式**  
 运行包含 sqlcmd 实用工具所支持的命令集的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。 有关详细信息，请参阅 [sqlcmd 操作指南主题](https://msdn.microsoft.com/library/dd7a2d2b-6327-4d77-ac5a-580d36073ad4)。  
  
## <a name="editor-tasks"></a>编辑器任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|介绍如何查看和使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器的基本功能。|[数据库引擎查询编辑器 (SQL Server Management Studio)](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)|  
|介绍如何查看和使用 MDX 查询编辑器的基本功能。|[MDX 查询编辑器（Analysis Services - 多维数据）](https://msdn.microsoft.com/library/777f2c23-1c1c-4b72-9d19-48a4866551f8)|  
|介绍如何查看和使用 DMX 查询编辑器的基本功能。|[DMX 查询编辑器（Analysis Services - 数据挖掘）](https://msdn.microsoft.com/library/7ac877a1-0f29-46b9-9a51-73b02172bef1)|  
|介绍如何查看和使用 XML/A 编辑器的基本功能。|[XML 编辑器 (SQL Server Management Studio)](../../relational-databases/scripting/xml-editor-sql-server-management-studio.md)|  
|介绍如何配置各种编辑器的选项，如行编号和 IntelliSense 选项。|[配置编辑器 (SQL Server Management Studio)](../../relational-databases/scripting/configure-editors-sql-server-management-studio.md)|  
|介绍可以在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中打开编辑器的各种方法。|[打开编辑器 (SQL Server Management Studio)](../../relational-databases/scripting/open-an-editor-sql-server-management-studio.md)|  
|介绍如何管理视图模式，如自动换行功能、拆分窗口或选项卡。|[管理编辑器和视图模式](../../relational-databases/scripting/manage-the-editor-and-view-mode.md)|  
|介绍如何设置格式设置选项，如隐藏文本或缩进。|[管理代码格式](../../relational-databases/scripting/manage-code-formatting.md)|  
|介绍如何通过如“渐进式搜索”或“转至”功能在编辑器窗口中导航文本内容。|[代码和文本定位](../../relational-databases/scripting/navigate-code-and-text.md)|  
|介绍如何设置各类语法的颜色编码选项，以便更容易读取复杂语句。|[查询编辑器中的颜色编码](../../relational-databases/scripting/color-coding-in-query-editors.md)|  
|介绍如何使用代码大纲显示模式隐藏复杂脚本中当前不处理的部分。|[代码大纲显示](../../relational-databases/scripting/code-outlining.md)|  
|介绍如何将文本从脚本的一个位置中拖出，然后放入一个新位置。|[拖放文本](../../relational-databases/scripting/drag-and-drop-text.md)|  
|介绍如何执行全局搜索和替换，例如在更改列名称时所要用到的全局搜索和替换。|[搜索和替换](../../relational-databases/scripting/search-and-replace.md)|  
|介绍如何设置书签，以便更容易地查找重要代码片段。|[管理书签](../../relational-databases/scripting/manage-bookmarks.md)|  
|介绍如何打印窗口或网格中的脚本或结果。|[打印代码和结果](../../relational-databases/scripting/print-code-and-results.md)|  
|介绍如何使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器中的 sqlcmd 功能。|[使用查询编辑器编辑 SQLCMD 脚本](../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)|  
|介绍如何使用 IntelliSense 功能，如在键入对象时自动完成对象名称或确保断点置于有效位置上。|[IntelliSense (SQL Server Management Studio)](../../relational-databases/scripting/intellisense-sql-server-management-studio.md)|  
|介绍如何使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器中的代码段。 代码段是常用语句或语句块的模板，可以自定义或扩展以包含特定站点代码段。|[Transact-SQL 代码片段](../../relational-databases/scripting/transact-sql-code-snippets.md)|  
|介绍如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器逐句运行代码，并查看诸如变量和参数中的值之类的调试信息。|[Transact-SQL 调试器](../../relational-databases/scripting/transact-sql-debugger.md)|  
|介绍如何为不同 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例设置自定义颜色，并将这些颜色设置为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器窗口中状态栏的背景。|[状态栏（数据库引擎查询编辑器）](../../relational-databases/scripting/status-bar-database-engine-query-editor.md)|  
  
## <a name="next-steps"></a>后续步骤

 [SQL Server Management Studio 键盘快捷键](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)