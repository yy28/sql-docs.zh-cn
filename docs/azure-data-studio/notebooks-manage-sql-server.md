---
title: 如何管理笔记本
description: 了解如何管理 Azure Data Studio 中的笔记本。 这包括打开笔记本、保存笔记本和更改 SQL 连接或 Python 内核。
author: markingmyname
ms.author: maghan
ms.reviewer: achatter, alayu, mikeray
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: 326e0b0afc4809d13cf2fdfdbd76f53dafe1cbb9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774581"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>如何管理 Azure Data Studio 中的笔记本

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文介绍如何在 Azure Data Studio 中打开和保存笔记本文件。 还演示了如何更改与 SQL Server 的连接或 Python 内核。

## <a name="open-a-notebook"></a>打开笔记本

可以通过多种方式打开“打开笔记本”对话框  。 可以使用“文件”菜单、“仪表板”和“命令面板”。 以下部分详细介绍了每种方法。

### <a name="file-menu"></a>“文件”菜单

从“文件”菜单中选择“打开文件”，可按 Ctrl+O（在 Windows 中）或 Cmd+O（在 Mac 中）  。

![选择“打开文件”，打开“打开文件”对话框](./media/notebooks-manage-sql-server/open-file-1.png)

### <a name="dashboard"></a>仪表板

单击仪表板中的“打开笔记本”，打开“打开文件”对话框  。

![在仪表板中选择“打开笔记本”，打开“打开文件”对话框](./media/notebooks-manage-sql-server/open-file-2.png) 

### <a name="command-palette"></a>命令面板

通过键入 Ctrl+Shift+P（在 Windows 中）  或 Cmd+Shift+P（在 Mac 中），使用命令面板中的命令“File:Open”。

![通过在命令面板中输入“File:Open”，打开“打开文件”对话框](./media/notebooks-manage-sql-server/open-file-3.png)

## <a name="save-a-notebook"></a>保存笔记本

目前有一种保存笔记本的方法。 选择笔记本工具栏中的“保存”  。

![通过选择笔记本工具栏中的“保存”来保存文件](./media/notebooks-manage-sql-server/save-file-1.png)

> [!NOTE]
> 以下方法目前不会保存对笔记本的更改：
>
> - “文件”菜单中的“文件保存”、“文件另存为...”和“文件全部保存”命令    。
> - 在命令面板中  输入的“File:Open”命令。

## <a name="change-the-sql-connection"></a>更改 SQL 连接

更改笔记本的 SQL 连接：

1. 选择笔记本工具栏中的“附加到”菜单，然后选择“更改连接”   。

   ![单击笔记本工具栏中的“附加到”菜单](./media/notebooks-manage-sql-server/select-attach-to-1.png)

2. 现在你可以选择一个最近的连接服务器，也可以输入新的连接详细信息进行连接。

   ![选择“附加到”菜单中的服务器](./media/notebooks-manage-sql-server/select-attach-to-2.png)

## <a name="change-the-python-kernel"></a>更改 Python 内核

首次打开 Azure Data Studio 时，将显示“为笔记本配置 Python”  页面。 可以选择以下任一项：

- “新 Python 安装”  ，用于为 Azure Data Studio 安装 Python 的新副本，或是
- “使用现有 Python 安装”  ，用于指定供 Azure Data Studio 使用的现有 Python 安装的路径

若要查看活动 Python 内核的位置和版本，请创建一个代码单元格，并运行以下 Python 命令：

```python
import os
import sys
print(sys.version_info)
print(os.path.dirname(sys.executable))
```

更改为不同的 Python 安装：

1. 在“文件”菜单中，选择“首选项”，然后选择“设置”    。
1. 在“扩展”下滚动到“笔记本配置”   。
1. 在“使用现有 Python”下，取消选中“笔记本使用的预先存在的 python 安装的本地路径”选项  。
1. 重启 Azure Data Studio。

显示“为笔记本配置 Python”  页面时，可以选择创建新 Python 安装或指定现有安装的路径。

## <a name="next-steps"></a>后续步骤

有关 Azure Data Studio 中的 SQL 笔记本的详细信息，请参阅[如何在 SQL Server 2019 中使用笔记本](notebooks-guidance.md)。
