---
title: 为 macOS 安装 azdata
titleSuffix: ''
description: 了解如何在 macOS 上安装 azdata 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c812600394546cba8adb0eacab59fa450b7c4bd2
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914906"
---
# <a name="install-azdata-on-macos"></a>在 macOS 上安装 `azdata`

对于 macOS 平台，可以通过 homebrew 包管理器安装 `azdata-cli`。 该 CLI 包已在以下 macOS 版本中测试： 
* 10.13 High Sierra
* 10.14 Mojave
* 10.15 Catalina

## <a name="install-with-homebrew"></a>使用 Homebrew 安装

```bash
brew tap microsoft/azdata-cli-release
brew update
brew install azdata-cli
```

>[!IMPORTANT]
>`azdata-cli` 依赖于 Homebrew `python3`、`freetds`、`unixodbc`、`zeromq` 包，并将安装它们。 `azdata-cli` 保证可与 Homebrew 上发布的这些最新版本的依赖项兼容。

## <a name="verify-install"></a>验证安装

```bash
azdata
azdata --version
```

## <a name="update"></a>更新

更新本地存储库信息，然后升级 `azdata-cli` 包。

```bash
brew tap microsoft/azdata-cli-release
brew update
brew upgrade azdata-cli
```

## <a name="uninstall"></a>卸载

使用 Homebrew 卸载 `azdata-cli` 包。

```bash
brew uninstall azdata-cli
```

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]？](../../big-data-cluster/big-data-cluster-overview.md)。

将 azdata 用于[已启用 Azure Arc 的数据服务](/azure/azure-arc/data/)
