---
title: 安装 azdata
titleSuffix: SQL Server big data clusters
description: 了解如何安装 azdata 工具以安装和管理大数据群集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 40338c4083241fedd113bca3a1beb839dbdd3fca
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75721676"
---
# <a name="install-azdata"></a>安装 `azdata`

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

`azdata` 是使用 Python 编写的命令行实用工具，可通过 REST API 启动和管理大数据群集。 

## <a name="find-latest-version"></a>查找最新版本

最新版本的文件列表始终位于 [https://aka.ms/azdata](https://aka.ms/azdata)。

若要查找你已安装的版本并查看是否需要更新，请运行 `azdata --version`。

## <a name="os-specific-instructions"></a>OS 特定说明

* [在 Windows 上安装](deploy-install-azdata-installer.md)
* [在 macOS 上安装](deploy-install-azdata-macos.md)
* 在 Linux 或[适用于 Linux 的 Windows 子系统 (WSL)](/windows/wsl/about/) 上安装
   * [在 Debian 或 Ubuntu 上使用 apt 进行安装](deploy-install-azdata-linux-package.md)
   * [在 RHEL 或 CentOS 上使用 yum 进行安装](deploy-install-azdata-yum.md)
   * [在 openSUSE 或 SLE 上使用 Zypper 进行安装](deploy-install-azdata-zypper.md)
   * [从脚本安装](deploy-install-azdata-pip.md)

[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
