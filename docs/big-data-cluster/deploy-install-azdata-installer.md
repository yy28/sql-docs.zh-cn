---
title: 安装 azdata 与 Windows Installer
titleSuffix: SQL Server big data clusters
description: 了解如何安装用于安装和管理[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (预览版) 的 azdata 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8dd5d2c7d0210880a82d774185a3f2a915608ec
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158142"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-with-windows-installer"></a>安装`azdata`以管理[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Windows Installer

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何在 Windows 上`azdata`安装 SQL Server 2019 大数据群集候选发布版本。 在 Windows 安装可用之前, `azdata`需要`pip`安装。

>对于 Linux (Ubuntu), 请[参阅`azdata`安装 with installer](./deploy-install-azdata-linux-package.md)。

此时, 没有可在其他操作系统或分发上安装`azdata`的包管理器。 对于这些平台, 请[参阅`azdata`安装而不安装程序包管理器](./deploy-install-azdata.md)。

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>安装`azdata` Microsoft Windows Installer

若要`azdata`在 Microsoft Windows Installer 上安装,

1. 如果`azdata`是使用`pip`安装的, 则删除。 如果`azdata`是使用 Windows Installer 安装的, 则继续执行下一步。
1. 使用`azdata` Windows Installer 安装。

### <a name="uninstall-if-previous-installation-done-with-pip"></a>如果上一次安装完成, 请卸载`pip`

如果安装了任何以前版本的**mssqlctl** , 请将其删除。 以下命令删除**mssqlctl**的 CTP 3.1 版本。

   ```bash
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

如果你安装了任何以前版本`azdata`的, 请务必先卸载该版本, 然后再安装最新版本。

   对于 CTP 3.2, 请运行以下命令。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

删除后,[在`azdata` Windows 上安装](#install-azdata-windows)。

>[!NOTE]
>如果先前的安装是使用 MSI 完成的, 则不需要在使用 MSI 安装程序之前卸载任何当前版本。

### <a id="install-azdata-windows"></a>安装 Windows Installer

使用 Windows Installer 在 Windows 上安装或`azdata`更新。

[下载WindowsInstaller`azdata` ](http://aka.ms/azdata-msi)。

当安装程序询问是否可以对您的计算机进行更改时, `Yes`请单击。

### <a name="uninstall-azdata-with-windows-installer"></a>卸载`azdata` Windows Installer

若要`azdata`卸载 Windows Installer, 请按照相应操作系统的说明进行操作。

| 平台      | 说明                                           |
| ------------- |--------------------------------------------------------|
| Windows 10    | 开始 > 设置 > 应用                                |
| Windows 8     | 启动 > 控制面板 "> 程序 > 卸载程序 |

要卸载的程序称为 **`Azdata CLI`** 。 选择此应用程序, 然后单击`Uninstall` "" 按钮。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息, 请参阅[什么[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]是？](big-data-cluster-overview.md)。
