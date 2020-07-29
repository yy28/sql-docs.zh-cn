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
ms.openlocfilehash: dbb484c6858e9024fdbbaa4d12c15480d7314bc9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784264"
---
# <a name="install-azdata"></a>安装 `azdata`

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

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
