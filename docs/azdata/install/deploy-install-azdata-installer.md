---
title: 使用 Windows Installer 安装 azdata
titleSuffix: ''
description: 了解如何通过安装程序安装 azdata 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a33e43386c44ec2ab60166ef57a502fc592c8d73
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914955"
---
# <a name="install-azdata-to-manage-big-data-clusters-2019-with-windows-installer"></a>使用 Windows Installer 安装 `azdata` 以管理 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/azdata.md)]

本文介绍如何在 Windows 上安装 `azdata`。 在 Windows 安装可用之前，需要使用 `pip` 安装 `azdata`。

>对于 Linux (Ubuntu)，请参阅[使用安装程序安装 `azdata`](./deploy-install-azdata-linux-package.md)。

目前，没有可在其他操作系统或发行版上安装 `azdata` 的包管理器。 对于这些平台，请参阅[不使用包管理器安装 `azdata`](./deploy-install-azdata.md)。

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>使用 Microsoft Windows Installer 安装 `azdata`

使用 Microsoft Windows Installer 安装 `azdata`：

1. 删除 `azdata`（如果已使用 `pip` 安装了它）。 如果已使用 Windows Installer 安装了 `azdata`，则继续执行下一步。
1. 使用 Windows Installer 安装 `azdata`。

### <a name="uninstall-if-previous-installation-done-with-pip"></a>卸载之前使用 `pip` 安装的版本

如果安装了以前的 `azdata` 版本，那么在安装最新版本之前，必须先卸载以前的版本。

   若要删除候选发布版本的 `azdata`，请运行以下命令。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

删除后，[在 Windows 上安装 `azdata`](#install-azdata-windows)。

>[!NOTE]
>如果以前的安装是使用 MSI 完成的，则不需要在使用 MSI 安装程序之前卸载任何当前版本。

### <a name="install-with-windows-installer"></a><a id="install-azdata-windows"></a>使用 Windows Installer 进行安装

使用 Windows Installer 在 Windows 上安装或更新 `azdata`。

[下载 `azdata` Windows Installer](https://aka.ms/azdata-msi)。

当安装程序询问它是否可以对你的计算机做出更改时，请单击 `Yes`。

### <a name="uninstall-azdata-with-windows-installer"></a>使用 Windows Installer 卸载 `azdata`

若要使用 Windows Installer 卸载 `azdata`，请按照相应操作系统的说明进行操作。

| 平台      | Instructions                                           |
| ------------- |--------------------------------------------------------|
| Windows 10| “开始”>“设置”>“应用”                                |
| Windows 8     | “开始”>“控制面板”>“程序”>“卸载程序” |

要卸载的程序名为 `Azdata CLI`。 选择此应用程序，然后单击 `Uninstall` 按钮。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]？](../../big-data-cluster/big-data-cluster-overview.md)

将 azdata 用于[已启用 Azure Arc 的数据服务](/azure/azure-arc/data/)
