---
title: Azure Data Studio 中使用 Python 内核的笔记本
description: 本教程介绍如何创建和运行 Python 笔记本。
author: garyericson
ms.author: garye
ms.reviewer: mikeray, alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: e4c431cba395b8e0c732fa7ac4ab96942cac7144
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728863"
---
# <a name="create-and-run-a-python-notebook"></a>创建和运行 Python 笔记本

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本教程演示如何使用 Python 内核在 Azure Data Studio 中创建和运行笔记本。

## <a name="prerequisites"></a>先决条件

- [已安装 Azure Data Studio](download-azure-data-studio.md)

## <a name="new-notebook"></a>新建笔记本

以下步骤演示如何在 Azure Data Studio 中创建笔记本文件：

1. 打开 Azure Data Studio。 如果系统提示连接到 SQL Server，则可以进行连接或单击“取消”  。

1. 在“文件”菜单中，选择“新建笔记本”。  

1. 对“内核”  选择“Python 3”  。

   :::image type="content" source="media/notebook-tutorial-python/set-kernel-and-attach-to-python.png" alt-text="设置内核":::

1. 如果系统提示配置 Python，请在“为笔记本配置 Python”  中选择：

   - “新 Python 安装”  ，用于为 Azure Data Studio 安装 Python 的新副本，或是
   - “使用现有 Python 安装”  ，用于指定现有 Python 安装的路径

## <a name="run-a-notebook-cell"></a>运行笔记本单元格

可以创建包含代码或文本的单元格。 可以就地运行代码单元格，结果会在单元格完成运行之后显示在笔记本中。 文本单元格使你可以随代码散置设置了格式的文档。

### <a name="code"></a>代码

选择工具栏中的“+代码”命令，添加一个新的 Python 代码单元格  。

:::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python.png" alt-text="笔记本工具栏":::

此示例将执行简单数学运算。

```python
a = 1
b = 2
c = a/b
print(c)
```
可通过单击单元格左侧的播放按钮来运行单元格。 结果在下面出现。

:::image type="content" source="media/notebook-tutorial-python/run-notebook-cell-python.png" alt-text="运行笔记本单元格":::

### <a name="text"></a>文本

选择工具栏中的“+文本”命令，添加一个新的文本单元格  。

:::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python-text.png" alt-text="笔记本工具栏":::

单元格更改为编辑模式，可以现在键入 markdown，会同时看到预览内容。

:::image type="content" source="media/notebook-tutorial-python/notebook-markdown-cell-python.png" alt-text="Markdown 单元格":::

选择文本单元格外部仅显示 markdown 文本。

:::image type="content" source="media/notebook-tutorial-python/notebook-markdown-preview-python.png" alt-text="Markdown 文本":::

## <a name="next-steps"></a>后续步骤

了解有关笔记本的详细信息：

- [如何通过 SQL Server 使用笔记本](notebooks-guidance.md)

- [创建和运行 SQL Server 笔记本](notebooks-tutorial-sql-kernel.md)

- [如何管理 Azure Data Studio 中的笔记本](notebooks-manage-sql-server.md)
