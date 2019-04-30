---
title: 创建可重用的代码段
titleSuffix: Azure Data Studio
description: 了解如何创建和使用 Azure 数据 Studio 中的 SQL 代码段
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e10b121ffc1afae83b767bcfdfe8e6765f990f4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63180689"
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-includename-sosincludesname-sos-shortmd"></a>创建和使用代码片段来快速创建中的 TRANSACT-SQL (T-SQL) 脚本 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

中的代码片段[!INCLUDE[name-sos](../includes/name-sos-short.md)]是模板，可以轻松快速地创建数据库和数据库对象。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供了若干 T-SQL 代码片段来帮助你快速生成正确的语法。 

也可以创建用户定义的代码片段。

## <a name="using-built-in-t-sql-code-snippets"></a>使用内置的 T-SQL 代码片段

1. 若要访问可用的代码片段，请键入*sql*在查询编辑器中打开的列表：

   ![代码段](media/code-snippets/sql-snippets.png)

1. 选择你想要使用，代码的段，并生成 T-SQL 脚本。 例如，选择*sqlCreateTable*:

   ![创建表的代码段](media/code-snippets/create-table.png)

1. 具有特定值更新突出显示的字段。 例如，替换*TableName*并*架构*替换为你的数据库的值：

   ![替换模板字段](media/code-snippets/table-from-snippet.png)

   如果你想要更改的字段不能再突出显示 （发生这种情况时将光标在编辑器中四处移动），右键单击你想要更改，并选择的词语**更改所有匹配项**:

   ![替换模板字段](media/code-snippets/change-all.png)

1. 更新或添加任何其他 T-SQL 的所需的所选的代码段。 例如，更新*Column1*， *Column2*，并添加更多的列。


 
## <a name="creating-sql-code-snippets"></a>创建 SQL 代码片段 

您可以定义自己的代码段。 若要打开的 SQL 代码段文件进行编辑：

1. 打开*命令面板*(**Shift + Ctrl + P**)，然后键入*截图*，并选择**首选项：打开用户代码片段**:

   ![替换模板字段](media/code-snippets/user-snippets.png)

1. 选择**SQL**:

   > [!NOTE]
   > [!INCLUDE[name-sos](../includes/name-sos-short.md)] 从 Visual Studio Code 继承其代码段功能，因此本文专门讨论如何使用 SQL 代码段。 有关详细信息，请参阅[创建自己的代码段](https://code.visualstudio.com/docs/editor/userdefinedsnippets)Visual Studio Code 文档中。 

   ![替换模板字段](media/code-snippets/select-sql.png)

1. 粘贴下面的代码插入*sql.json*:

   ```sql
   {
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
   }
   ```

1. 保存 sql.json 文件。
1. 通过单击打开新查询编辑器窗口**Ctrl + N**。
2. 类型**sql**，并查看您刚添加的; 两个用户代码片段*sqlCreateTable2*并*sqlSelectTop5*。

选择一个新的代码段和对其进行测试运行 ！


## <a name="additional-resources"></a>其他资源

有关 SQL 编辑器的信息，请参阅[代码编辑器教程](tutorial-sql-editor.md)。
