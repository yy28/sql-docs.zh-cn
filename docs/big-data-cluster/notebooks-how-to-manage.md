---
title: 管理笔记本：Azure Data Studio
titleSuffix: SQL Server Big Data Clusters
description: 了解如何管理 Azure Data Studio 中的笔记本。 包括打开笔记本、保存笔记本和更改大数据群集连接。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8cf37ff6a4ad5e2b627fa5d968391cc5a7597a4a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244090"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>如何管理 Azure Data Studio 中的笔记本

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何使用 SQL Server 在 Azure Data Studio 中打开和保存笔记本文件。 还演示了如何更改与 SQL Server 大数据群集的连接。

## <a name="prerequisites"></a>必备条件

本文假定你已有一个要在 Azure Data Studio 中使用的笔记本。 若要创建笔记本，请参阅[如何在 SQL Server 中使用笔记本](notebooks-guidance.md)。 若要使用 Azure Data Studio 中的笔记本，则必须满足以下先决条件：

- [部署大数据群集](quickstart-big-data-cluster-deploy.md)。
- [SQL Server 2019 大数据工具](deploy-big-data-tools.md)：
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
   - **kubectl**

## <a name="open-a-notebook"></a>打开笔记本

可以通过多种方式打开“打开笔记本”对话框  。 可以使用“文件”菜单、“仪表板”和“命令面板”。 以下部分详细介绍了每种方法。

### <a name="file-menu"></a>“文件”菜单

从“文件”菜单中选择“打开文件”，可按 Ctrl+O（在 Windows 中）或 Cmd+O（在 Mac 中）  。

![选择“打开文件”，打开“打开文件”对话框](./media/notebooks-how-to-manage/open-file-1.png) 

### <a name="dashboard"></a>仪表板

单击仪表板中的“打开笔记本”，打开“打开文件”对话框  。

![在仪表板中选择“打开笔记本”，打开“打开文件”对话框](./media/notebooks-how-to-manage/open-file-2.png) 

### <a name="command-palette"></a>命令面板

通过键入 Ctrl+Shift+P（在 Windows 中）或 Cmd+Shift+P（在 Mac 中），使用命令面板中的命令“File:Open”  。

![通过在命令面板中输入“File:Open”，打开“打开文件”对话框](./media/notebooks-how-to-manage/open-file-3.png)

## <a name="save-a-notebook"></a>保存笔记本

当前有一种方法可以保存笔记本。 必须从笔记本工具栏中选择“保存”  。

![单击笔记本工具栏中的“保存”来保存文件](./media/notebooks-how-to-manage/save-file-1.png)

> [!NOTE]
> 以下方法目前不会保存对笔记本的更改：
>
> - “文件”菜单中的“文件保存”、“文件另存为...”和“文件全部保存”命令    。
> - 在命令面板中输入的“File:Open”命令  。

## <a name="change-the-big-data-cluster"></a>更改大数据群集

更改笔记本的 SQL Server 大数据群集：

1. 单击笔记本工具栏中的“附加到”菜单  。

   ![单击笔记本工具栏中的“附加到”菜单](./media/notebooks-how-to-manage/select-attach-to-1.png)

2. 单击“附加到”菜单中的服务器  。

   ![选择“附加到”菜单中的服务器](./media/notebooks-how-to-manage/select-attach-to-2.png)

## <a name="next-steps"></a>后续步骤

有关 Azure Data Studio 中的笔记本的详细信息，请参阅[如何在 SQL Server 2019 中使用笔记本](notebooks-guidance.md)。
