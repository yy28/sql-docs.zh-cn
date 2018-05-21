---
title: 在 SQL 操作 Studio （预览版） 中创建的代码段 |Microsoft 文档
description: 了解如何创建和使用 SQL 操作 Studio （预览版） 中的 SQL 代码段
ms.custom: tools|sos
ms.date: 11/15/2017
ms.reviewer: alayu; sstein
ms.prod: sql
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8cd2dc80f7a719f82bd4ff09729cbbd5dfb4186
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-includename-sosincludesname-sos-shortmd"></a>创建和使用代码片段来快速创建中的 TRANSACT-SQL (T-SQL) 脚本 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

代码片段中的[!INCLUDE[name-sos](../includes/name-sos-short.md)]更简便地的模板创建数据库和数据库对象。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供若干的 T-SQL 代码段，以帮助你快速生成正确的语法。 

也可以创建用户定义代码段。

## <a name="using-built-in-t-sql-code-snippets"></a>使用内置的 T-SQL 代码片段

1. 若要访问可用的代码段，请键入*sql*在查询编辑器中打开的列表：

   ![代码段](media/code-snippets/sql-snippets.png)

1. 选择你想要使用，代码的段，并生成 T-SQL 脚本。 例如，选择*sqlCreateTable*:

   ![创建表代码段](media/code-snippets/create-table.png)

1. 使用特定的值更新突出显示的字段。 例如，对于替换*TableName*和*架构*替换为你的数据库的值：

   ![替换模板字段](media/code-snippets/table-from-snippet.png)

   如果你想要更改的字段不再突出显示 （发生这种情况时移动光标绕编辑器），右键单击要更改，并选择所需的单词**更改所有匹配项**:

   ![替换模板字段](media/code-snippets/change-all.png)

1. 更新或添加任何其他 T-SQL 的所需的所选的代码段。 例如，更新*Column1*， *Column2*，并添加更多的列。


 
## <a name="creating-sql-code-snippets"></a>创建 SQL 代码片段 

你可以定义自己的代码段。 若要打开以进行编辑的 SQL 代码段文件：

1. 打开*命令控制板*(**Shift + Ctrl + P**)，并键入*代码段*，然后选择**首选项： 打开用户代码段**:

   ![替换模板字段](media/code-snippets/user-snippets.png)

1. 选择**SQL**:

   > [!NOTE]
   > [!INCLUDE[name-sos](../includes/name-sos-short.md)] 从 Visual Studio Code 继承其代码段功能，因此这篇文章专门讨论了如何使用 SQL 代码段。 有关详细信息，请参阅[创建自己的代码段](https://code.visualstudio.com/docs/editor/userdefinedsnippets)Visual Studio Code 文档中。 

   ![替换模板字段](media/code-snippets/select-sql.png)

1. 粘贴下面的代码插入*sql.json*:

   ```sql
   "Select top 5": {
    "prefix": "sqlSelectTop5",
    "body": "SELECT TOP 5 * FROM ${1:TableName}",
    "description": "User-defined snippet example 1"
    },
    "Create Table snippet":{
    "prefix": "sqlCreateTable2",
    "body": [
    "-- Create a new table called '${1:TableName}' in schema '${2:SchemaName}'",
    "-- Drop the table if it already exists",
    "IF OBJECT_ID('$2.$1', 'U') IS NOT NULL",
    "DROP TABLE $2.$1",
    "GO",
    "-- Create the table in the specified schema",
    "CREATE TABLE $2.$1",
    "(",
    "   $1Id INT NOT NULL PRIMARY KEY, -- primary key column",
    "   Column1 [NVARCHAR](50) NOT NULL,",
    "   Column2 [NVARCHAR](50) NOT NULL",
    "   -- specify more columns here",
    ");",
    "GO"
    ],
   "description": "User-defined snippet example 2"
   }
   ```

1. 保存 sql.json 文件。
1. 通过单击打开一个新的查询编辑器窗口**Ctrl + N**。
2. 类型**sql**，并查看你刚添加; 的两个用户代码段*sqlCreateTable2*和*sqlSelectTop5*。

选择一个新的代码段，并为其提供测试运行 ！


## <a name="additional-resources"></a>其他资源

有关 SQL 编辑器的信息，请参阅[代码编辑器教程](tutorial-sql-editor.md)。