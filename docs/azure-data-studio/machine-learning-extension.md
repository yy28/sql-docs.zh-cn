---
title: 机器学习扩展（预览版）
titleSuffix: Azure Data Studio
description: 借助 Azure Data Studio 的机器学习扩展，你可以管理包、导入机器学习模型、作出预测以及创建笔记本，以运行 SQL 数据库试验。
ms.date: 05/19/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e6b38724e2cb8fde7fe38a544c3f87fba3cebd45
ms.sourcegitcommit: 48d60fe6b6991303a88936fb32322c005dfca2d8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85352414"
---
# <a name="machine-learning-extension-preview-for-azure-data-studio"></a>Azure Data Studio 的机器学习扩展（预览版）

借助 [Azure Data Studio](what-is.md) 的机器学习扩展，你可以管理包、导入机器学习模型、作出预测以及创建笔记本，以运行 SQL 数据库试验。 此扩展当前处于预览状态。

## <a name="prerequisites"></a>先决条件

需要在运行 Azure Data Studio 的计算机上安装以下必备组件。

- [Python 3](https://www.python.org/downloads/)。 安装 Python 后，需要在[扩展设置](#settings)下指定 Python 安装的本地路径。 如果在 Azure Data Studio 中使用了 [Python 内核笔记本](notebooks-tutorial-python-kernel.md)，则扩展将默认使用笔记本中的路径。

- 适用于 Windows、macOS 或 Linux 的 [Microsoft ODBC Driver 17 for SQL Server](../connect/odbc/download-odbc-driver-for-sql-server.md)。

- [R 3.5](https://www.r-project.org/)（可选）。 当前不支持 3.5 以外的其他版本。 安装 R 3.5 后，需要启用 R 并在[扩展设置](#settings)下指定 R 安装的本地路径。 仅当要管理数据库中的 R 包时，才需要此项。

## <a name="install-the-extension"></a>安装扩展

若要在 Azure Data Studio 中安装机器学习扩展，请按照以下步骤操作。

1. 在 Azure Data Studio 中打开扩展管理器。 可以选择扩展图标，也可以在“视图”菜单中选择“扩展”。

1. 选择“机器学习”扩展并查看其详细信息。

1. 单击“安装”。

1. 单击“重载”以启用扩展。 仅在首次安装扩展时才需要此步骤。

<a name="settings"></a>

## <a name="extension-settings"></a>扩展设置

若要更改机器学习扩展的设置，请按照以下步骤操作。

1. 在 Azure Data Studio 中打开扩展管理器。 可以选择扩展图标，也可以在“视图”菜单中选择“扩展”。

1. 在“已启用”的扩展下找到“机器学习”扩展 。

1. 单击“管理”图标。

1. 单击“扩展设置”图标。

扩展设置如下所示：

:::image type="content" source="media/machine-learning-extension/ml-extension-settings.png" alt-text="机器学习扩展设置":::

### <a name="enable-python"></a>启用 Python

若要在数据库中使用机器学习扩展以及 Python 包管理，请按照以下步骤操作。

> [!IMPORTANT]
> 即使不希望在数据库功能中使用 Python 包管理，机器学习扩展也需要启用 Python 并将其配置为可使用大多数功能。

1. 确保“机器学习: 启用 Python”已启用。 默认情况下，此设置处于启用状态。

1. 在“机器学习: Python 路径”下提供预先存在的 Python 安装的路径。 这可以是 Python 可执行文件的完整路径，也可以是该可执行文件所在的文件夹。 如果在 Azure Data Studio 中使用了 [Python 内核笔记本](notebooks-tutorial-python-kernel.md)，则扩展将默认使用笔记本中的路径。

### <a name="enable-r"></a>启用 R

若要在数据库中使用机器学习扩展进行 R 包管理，请按照以下步骤操作。

1. 确保“机器学习: 启用 R”已启用。 默认情况下，此设置处于禁用状态。

1. 在“机器学习: R 路径”下提供预先存在的 R 安装的路径。 这必须是 R 可执行文件的完整路径。 

## <a name="use-the-machine-learning-extension"></a>使用机器学习扩展

若要在 Azure Data Studio 中使用机器学习扩展，请按照以下步骤操作。

1. 在 Azure Data Studio 中打开连接。

1. 右键单击服务器，并选择“管理”。

1. 单击左侧“常规”下的菜单中的“机器学习” 。

单击“下一步”下的链接，了解如何使用机器学习扩展在数据库中管理包、作出预测以及导入模型。

## <a name="next-steps"></a>后续步骤

- [管理数据库中的包](machine-learning-extension-manage-packages.md)
- [作出预测](machine-learning-extension-predictions.md)
- [导入或查看模型](machine-learning-extension-import-view-models.md)
- [Azure Data Studio 中的笔记本](notebooks-guidance.md)
- [SQL 机器学习文档](../machine-learning/index.yml)
- [在 SQL Edge（预览版）中将机器学习和 AI 与 ONNX 结合使用](/azure/azure-sql-edge/onnx-overview)
