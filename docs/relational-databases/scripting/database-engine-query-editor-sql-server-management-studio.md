---
title: "数据库引擎查询编辑器 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 40ac7dd736d0366fe5cb564719a375e2e6a6a43d
ms.lasthandoff: 04/11/2017

---
# <a name="database-engine-query-editor-sql-server-management-studio"></a>数据库引擎查询编辑器 (SQL Server Management Studio)
  使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器可以创建和运行包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的脚本。 此编辑器还支持包含 **sqlcmd** 命令的正在运行的脚本。  
  
## <a name="transact-sql-f1-help"></a>Transact-SQL F1 帮助  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器支持当您选择 F1 时将您链接到特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的参考主题。 为此，突出显示 Transact-SQL 语句的名称，然后选择 F1。 接着，帮助搜索引擎将搜索具有与突出显示的字符串匹配的 F1 帮助属性的主题。  
  
 如果帮助搜索引擎找不到具有与突出显示的字符串完全匹配的 F1 帮助关键字的主题，则无法显示该主题。 在这种情况下，有两种方法可以找到所需的帮助：  
  
-   将您突出显示的编辑器字符串复制并粘贴到 SQL Server 联机丛书的搜索选项卡中，并执行搜索。  
  
-   仅突出显示 Transact-SQL 语句中可能与应用于主题的 F 帮助关键字匹配的部分，然后再次选择 F1。 搜索引擎要求突出显示的字符串与分配给主题的 F1 帮助关键字之间完全匹配。 如果突出显示的字符串包含对于您的环境是唯一的元素（如列或参数名称），则搜索引擎将不会获得匹配项。 要突出显示的字符串的示例包括：  
  
    -   Transact-SQL 语句的名称，如 SELECT、CREATE DATABASE 或 BEGIN TRANSACTION。  
  
    -   内置函数的名称，如 SERVERPROPERTY 或 @@VERSION。  
  
    -   系统存储过程表或视图的名称，如 sys.data_spaces 或 sp_tableoption。  
  
## <a name="working-with-the-database-engine-query-editor"></a>使用数据库引擎查询编辑器  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]查询编辑器是在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中实现的四个编辑器之一。 对于在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器中实现的功能以及使用此编辑器可以执行的主要任务的说明，请参阅[查询和文本编辑器 (SQL Server Management Studio)](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)。  
  
## <a name="sql-editor-toolbar"></a>SQL 编辑器工具栏  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器打开时，SQL 编辑器工具栏上显示以下按钮：  
  
 **连接**  
 打开“连接到服务器”对话框。 此对话框用于建立与服务器的连接。  
  
 **断开连接**  
 断开当前查询编辑器与服务器之间的连接。  
  
 **更改连接**  
 打开“连接到服务器”对话框。 此对话框用于建立与另一个服务器的连接。  
  
 **使用当前连接新建查询**  
 打开新的查询编辑器窗口并使用当前查询编辑器窗口的连接信息。  
  
 **可用数据库**  
 将连接更改到同一服务器上的其他数据库。  
  
 **Execute**  
 执行所选的代码，如果没有选择任何代码，则执行查询编辑器中的全部代码。  
  
 **调试**  
 启用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器。 此调试器支持调试操作，例如设置断点、监视变量和单步执行代码。  
  
 **取消执行查询**  
 向服务器发送取消请求。 有些查询不能立即取消，而必须等待适当的取消条件。 取消事务时，在回滚事务期间可能发生延迟。  
  
 **分析**  
 检查所选代码的语法。 如果没有选择任何代码，则检查查询编辑器窗口中全部代码的语法。  
  
 **显示估计的执行计划**  
 从查询处理器中请求查询执行计划而不实际执行查询，并在“执行计划”窗口中显示该计划。 此计划使用索引统计值作为查询执行的各个部分预期返回的行数估计值。 实际使用的查询计划可能与估计的执行计划不同。 如果返回的行数与估计值有明显差距，并且查询处理器更改了执行计划以提高其效率，就会发生这种情况。  
  
 **查询选项**  
 打开“查询选项”对话框。 此对话框用于配置查询执行和查询结果的默认选项。  
  
 **IntelliSense 已启用**  
 指定 IntelliSense 功能在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器中是否可用。  
  
 **包含实际的执行计划**  
 执行查询，返回查询结果和用于查询的执行计划。 这些内容在 **“执行计划”** 窗口中显示为图形查询计划。  
  
 **包括客户端统计信息**  
 提供一个“客户端统计信息”窗口，其中包含有关查询、网络数据包以及查询占用时间的统计信息。  
  
 **以文本格式显示结果**  
 在“结果”窗口中以文本格式返回查询结果。  
  
 **以网格显示结果**  
 在“结果”窗口中以一个或多个网格的形式返回查询结果。  
  
 **将结果保存到文件**  
 在执行查询时，“保存结果”对话框将会打开。 在 **“保存于”**中，选择要将文件保存到的文件夹。 在 **“文件名”**中键入文件名，然后单击 **“保存”** 将查询结果保存为具有 .rpt 扩展名的 **“报表”** 文件。 对于高级选项，请单击“保存”按钮上的向下箭头，再单击“编码保存”。  
  
 **注释选定内容**  
 在当前行的开头处添加一个注释运算符 (--)，以对该行进行注释。  
  
 **取消注释选定内容**  
 删除当前行开头处的任何注释运算符 (--)，以使该行成为一个活动的源语句。  
  
 **减少行缩进**  
 删除行开头处的空格，从而使该行文本向左移动。  
  
 **增加行缩进**  
 在行开头处插入空格，从而使该行文本向右移动。  
  
 **指定模板参数的值**  
 打开一个对话框，在此对话框中可以指定存储过程或函数中参数的值。  
  
 通过依次选择 **“视图”** 菜单、 **“工具栏”**和 **“SQL 编辑器”**，还可添加 SQL 编辑器工具栏。 如果在没有打开任何 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器窗口时添加 SQL 编辑器工具栏，则所有按钮都不可用。  
  
## <a name="sql-editor-toolbar"></a>SQL 编辑器工具栏  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器窗口打开后，可以通过以下方法添加调试工具栏：在 **“视图”** 菜单上选择 **“工具栏”**，然后选择 **“调试”**。 如果在没有打开任何 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器窗口的情况下添加调试工具栏，则所有按钮都不可用。  
  
 **Continue**  
 运行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器窗口中的代码，直到遇到断点。  
  
 **全部中断**  
 将调试器设置为发生中断时中断调试器附加到的所有进程。  
  
 **停止调试**  
 使选定的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器窗口脱离调试模式，并还原标准执行模式。  
  
 **显示下一语句**  
 将光标移动到要执行的下一个语句。  
  
 **逐语句**  
 运行下一个语句。 如果该语句调用 Transact-SQL 存储过程、函数或触发器，则调试器会显示一个包含该模块的代码的新“查询编辑器”窗口。 该窗口处于调试模式，并在模块中的第一个语句上暂停执行。 然后，您可以在模块中移动，例如，设置断点或逐句通过代码。  
  
 **逐过程**  
 运行下一个语句。 如果该语句调用了 Transact-SQL 存储过程、函数或触发器，则模块会运行，直到完成运行，并将结果返回到调用代码。 如果确认模块中没有错误，可以逐过程执行。 在调用模块的后面的语句上暂停执行。  
  
 **跳出**  
 后退到下一个最高调用级别（函数、存储过程或触发器）。 在调用存储过程、函数或触发器的后面的语句上暂停执行。  
  
 **Windows**  
 打开“断点”窗口或“即时”窗口。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Management Studio 键盘快捷键](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
