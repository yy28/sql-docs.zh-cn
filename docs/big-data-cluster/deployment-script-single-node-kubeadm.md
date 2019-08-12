---
title: 使用 bash 脚本部署到单个节点 kubeadm 群集
titleSuffix: SQL Server big data clusters
description: 使用 bash 部署脚本将 SQL Server 2019 大数据群集（预览版）部署到单节点 kubeadm 群集。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 37017221b636146a003f8af8890c655ed605bca9
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68473069"
---
# <a name="deploy-with-a-bash-script-to-a-single-node-kubeadm-cluster"></a>使用 bash 脚本部署到单个节点 kubeadm 群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在本教程中，你将使用示例 bash 部署脚本部署使用 kubeadm 的单节点 Kubernetes 群集，并在其上部署 SQL Server 大数据群集。  

## <a name="prerequisites"></a>必备条件

- Vanilla Ubuntu 18.04 或 16.04 服务器 VM  。 所有依赖项都由脚本设置，你可以从 VM 内部运行该脚本。

  > [!NOTE]
  > 尚不支持使用 Azure VM。

- VM 应至少具有 8 个 CPU、64 GB 的 RAM 和 100 GB 磁盘空间。 在拉取所有大数据群集 Docker 映像后，将剩下 50 GB 用于在所有组件中使用的数据和日志。

## <a name="instructions"></a>Instructions

1. 在 VM 上下载计划用于部署的脚本。

   ```bash
   curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
   ```

2. 使用以下命令使该脚本可执行。

   ```bash
   chmod +x setup-bdc.sh
   ```

3. 使用 sudo 运行脚本  。

   ```bash
   sudo ./setup-bdc.sh
   ```

   出现提示时，请输入供以下外部终结点使用的密码：控制器、SQL Server master 和网关。 控制器用户名默认为 admin  。

4. 设置 azdata 工具的别名  。

   ```bash
   source ~/.bashrc
   ```

5. 验证别名是否正常工作。

   ```bash
   azdata --version
   ```

## <a name="next-steps"></a>后续步骤

按照[本教程](tutorial-load-sample-data.md)开始使用大数据群集。
