---
title: 使用 Azure Data Studio 笔记本部署 SQL Server 大数据群集
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: 使用 Azure Data Studio 中的笔记本部署大数据群集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d68baa615f384dd5afb665f29decb6d72113c5a3
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028572"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>使用 Azure Data Studio 笔记本部署 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 为包含部署笔记本的 Azure Data Studio 提供扩展。 部署笔记本包含可在 Azure Data Studio 中用于创建 SQL Server 大数据群集的文档和代码。

[笔记本](notebooks-guidance.md)最初作为开放源代码项目实现，现已应用于[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download)。 可以在文本单元格中使用 markdown 作为文本，并使用其中一个可用核心在代码单元格中编写代码。

可以使用笔记本为 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 部署大数据群集。

## <a name="prerequisites"></a>先决条件

要启动笔记本，需要满足以下必备条件：

* 已安装[Azure Data Studio 预览体验](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)版本的最新版本
* 已在 Azure Data Studio 中安装 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 扩展

除上述内容外，部署 SQL Server 2019 大数据群集还需要：

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="launch-the-notebook"></a>启动笔记本

1. 启动 Azure Data Studio 内部人员。

1. 在“连接”选项卡上，单击“...”，然后选择“部署 SQL Server 大数据群集...”。

   ![AI 和 ML](media/deploy-notebooks/deploy-notebooks-1.png)

1. 在“选项”下的“部署目标”中，选择“新建 Azure Kubernetes 群集”或“现有 Azure Kubernetes 服务群集”。

1. 单击 "**选择**按钮"。

1. 此操作将启动一个对话框以收集用户输入, 提供所需的信息并查看默认值。

1. 单击 "**打开笔记本**" 按钮。
此操作会启动相应的笔记本。 要完成部署，请遵循笔记本中的说明在现有或新建的 Azure Kubernetes 服务群集上为 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 部署大数据群集。

## <a name="next-steps"></a>后续步骤

有关部署的详细信息，请参阅 [SQL Server 大数据群集部署指南](deployment-guidance.md)。
