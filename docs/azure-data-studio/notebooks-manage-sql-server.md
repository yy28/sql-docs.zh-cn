---
title: 管理 SQL Server 笔记本
description: 了解如何管理 Azure Data Studio 中的笔记本。 包括打开笔记本、保存笔记本和更改大数据群集连接。
author: markingmyname
ms.author: maghan
ms.reviewer: achatter, alayu, mikeray
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 03/30/2020
ms.openlocfilehash: 9b071a9d1b9e770e1443e5df539208baa4399a30
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531590"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>如何管理 Azure Data Studio 中的笔记本

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何使用 SQL Server 在 Azure Data Studio 中打开和保存笔记本文件。 还演示了如何更改与 SQL Server 的连接。

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

## <a name="change-the-connection"></a>更改连接

更改笔记本的连接：

1. 选择笔记本工具栏中的“附加到”菜单，然后选择“更改连接”   。

   ![单击笔记本工具栏中的“附加到”菜单](./media/notebooks-manage-sql-server/select-attach-to-1.png)

2. 现在你可以选择一个最近的连接服务器，也可以输入新的连接详细信息进行连接。

   ![选择“附加到”菜单中的服务器](./media/notebooks-manage-sql-server/select-attach-to-2.png)

## <a name="next-steps"></a>后续步骤

有关 Azure Data Studio 中的笔记本的详细信息，请参阅[如何在 SQL Server 2019 中使用笔记本](notebooks-guidance.md)。
