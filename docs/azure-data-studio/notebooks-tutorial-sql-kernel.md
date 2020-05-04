---
title: Azure Data Studio 中使用 SQL 内核的笔记本
description: 本教程介绍如何创建和运行 SQL Server 笔记本。
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray, alayu
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 03/30/2020
ms.openlocfilehash: 70136c114fe1d4e9421400eff5f171a70289098c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "82178688"
---
# <a name="create-and-run-a-sql-server-notebook"></a>创建和运行 SQL Server 笔记本

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教程演示如何使用 SQL Server 在 Azure Data Studio 中创建和运行笔记本。

## <a name="prerequisites"></a>先决条件

- [已安装 Azure Data Studio](download-azure-data-studio.md)
- 已安装 SQL Server
  - [Windows](../database-engine/install-windows/install-sql-server.md)
  - [Linux](../linux/sql-server-linux-setup.md)

## <a name="new-notebook"></a>新建笔记本

以下步骤演示如何在 Azure Data Studio 中创建笔记本文件：

1. 在 Azure Data Studio 中，连接到你的 SQL Server。

2. 在“服务器”窗口中的“连接”下进行选择   。 然后选择“新建笔记本”  。

   ![打开笔记本](media/notebook-tutorial/azure-data-studio-open-notebook.png)

3. 等待要填充的 Kernel 和目标上下文（“附加到”）   。 确认“内核”设置为“SQL”，并设置 SQL Server 的“附加到”（在本例中为 localhost）     。

   ![设置 Kernel 和“附加到”](media/notebook-tutorial/set-kernel-and-attach-to.png)

## <a name="run-a-notebook-cell"></a>运行笔记本单元格

可以通过按单元格左侧的“播放”按钮来运行每个笔记本单元格。 单元格完成运行后，结果会显示在笔记本中。

### <a name="code"></a>代码

选择工具栏中的“+代码”命令，添加一个新的代码单元格  。

![笔记本工具栏](media/notebooks-guidance/notebook-toolbar.png)

此示例将创建一个新的数据库。

```sql
USE master
GO

   -- Drop the database if it already exists
IF  EXISTS (
        SELECT name
        FROM sys.databases
        WHERE name = N'TestNotebookDB'
   )
DROP DATABASE TestNotebookDB
GO

-- Create the database
CREATE DATABASE TestNotebookDB
GO
```

   ![运行笔记本单元格](media/notebook-tutorial/run-notebook-cell.png)

如果运行返回结果的脚本，则可以将结果保存为不同的格式。

- 另存为 CSV
- 另存为 Excel
- 另存为 JSON
- 另存为 XML

在本例中，我们返回结果 [PI](../t-sql/functions/pi-transact-sql.md)。

```sql
SELECT PI() AS PI;
GO
```

![运行笔记本单元格](media/notebook-tutorial/run-notebook-cell-2.png)

### <a name="text"></a>文本

选择工具栏中的“+文本”命令，添加一个新的文本单元格  。

![笔记本工具栏](media/notebooks-guidance/notebook-toolbar.png)

单元格更改为编辑模式，现在键入 markdown，你可以同时看到预览内容

![Markdown 单元格](media/notebooks-guidance/notebook-markdown-cell.png)

选择文本单元格外部即可显示 markdown 文本。

![Markdown 文本](media/notebooks-guidance/notebook-markdown-preview.png)

## <a name="next-steps"></a>后续步骤

了解有关笔记本的详细信息：

- [如何通过 SQL Server 使用笔记本](notebooks-guidance.md)

- [如何管理 Azure Data Studio 中的笔记本](notebooks-manage-sql-server.md)

- [使用 Spark 运行示例笔记本](../big-data-cluster/notebooks-tutorial-spark.md)