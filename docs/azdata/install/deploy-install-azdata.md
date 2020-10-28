---
title: 安装 Azure Data CLI (azdata)
titleSuffix: ''
description: 了解如何安装 Azure Data CLI (azdata) 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 82aa3a2795328804a10a76e9ecd8af80f3bf7152
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257390"
---
# <a name="install-azure-data-cli-azdata"></a>安装 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] 是使用 Python 编写的命令行实用工具，可通过 REST API 启动和管理数据服务。 

## <a name="find-latest-version"></a>查找最新版本

最新版本的文件列表始终位于 [https://aka.ms/azdata](https://aka.ms/azdata)。

若要查找你已安装的版本并查看是否需要更新，请运行 `azdata --version`。

## <a name="os-specific-instructions"></a>OS 特定说明

* [在 Windows 上安装](../install/deploy-install-azdata-installer.md)
* [在 macOS 上安装](../install/deploy-install-azdata-macos.md)
* 在 Linux 或[适用于 Linux 的 Windows 子系统 (WSL)](/windows/wsl/about/) 上安装
   * [在 Debian 或 Ubuntu 上使用 apt 进行安装](../install/deploy-install-azdata-linux-package.md)
   * [在 RHEL 或 CentOS 上使用 yum 进行安装](../install/deploy-install-azdata-yum.md)
   * [在 openSUSE 或 SLE 上使用 Zypper 进行安装](../install/deploy-install-azdata-zypper.md)
   * [从脚本安装](../install/deploy-install-azdata-pip.md)

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="next-steps"></a>后续步骤

有关在大数据群集中使用 azdata 的信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]？](../../big-data-cluster/big-data-cluster-overview.md)

将 azdata 用于[已启用 Azure Arc 的数据服务](/azure/azure-arc/data/)
