---
title: 使用 yum 安装 azdata
titleSuffix: ''
description: 了解如何通过 yum 安装 azdata 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 35afcae7bb5cef31bd59b53688c2eec07ee74a7c
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257500"
---
# <a name="install-azure-data-cli-azdata-with-yum"></a>使用 yum 安装 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

带有 `yum` 的 Linux 分发版有 `azdata-cli` 包。 该 CLI 包已在使用 `yum` 的 Linux 版本中测试：

- RHEL 7 和 RHEL 8

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-yum"></a>使用 yum 进行安装

>[!IMPORTANT]
> `azdata-cli` 的 RPM 包依赖于 python3 包。 在你的系统上，这可能是早于所要求的 Python 3.6.x  的 Python 版本。 如果这对你来说是问题，请找到一个替代 python3 包，或按照使用 [`pip`](../install/deploy-install-azdata-pip.md) 的手动安装说明执行操作。

1. 安装必要的依赖项以安装 `azdata-cli`。

   ```bash
   sudo yum install -y curl
   ```

1. 导入 Microsoft 存储库密钥。

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. 创建本地存储库信息。

   对于 RHEL 7 客户端运行：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```
  
   对于 RHEL 8 客户端运行：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/prod.repo
   ```

1. 安装 `azdata-cli`。

   ```bash
   sudo yum install azdata-cli
   ```

## <a name="verify-install"></a>验证安装

```bash
azdata
azdata --version
```

## <a name="update"></a>更新

使用 `yum update` 命令更新 `azdata-cli`。

```bash
sudo yum update azdata-cli
```

## <a name="uninstall"></a>卸载

1. 从系统中删除包。

   ```bash
   sudo yum remove azdata-cli
   ```

1. 如果不打算重新安装 `azdata-cli`，请删除存储库信息。

   ```bash
   sudo rm /etc/yum.repos.d/azdata-cli.repo
   ```

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]？](../../big-data-cluster/big-data-cluster-overview.md)。

将 azdata 用于[已启用 Azure Arc 的数据服务](/azure/azure-arc/data/)
