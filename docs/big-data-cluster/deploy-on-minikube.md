---
title: 配置 minikube
titleSuffix: SQL Server big data clusters
description: 了解如何在单台计算机上为 SQL Server 2019 大数据群集（预览版）部署配置 minikube。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6c2261b5cfbbe590c76ce410da4b95ee678a20b5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958478"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>为 SQL Server 大数据群集部署配置 minikube

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何在单台计算机上为 SQL Server 2019 大数据群集（预览版）部署配置 **minikube**。 Minikube 是一种工具，可让用户在单台计算机（如笔记本电脑或台式机）上轻松运行 Kubernetes。 Minikube 在笔记本电脑上的 VM 内运行单节点 Kubernetes 群集，以供想要试用 Kubernetes 或使用它进行日常开发的用户使用。 

## <a name="prerequisites"></a>必备条件

- 32 GB 内存（建议 64 GB）。

- 如果计算机仅具有建议的最小内存，则将群集部署配置为仅包含 1 个计算池实例、1 个数据池实例和 1 个存储池实例。 此配置应该仅用于数据的持续性和可用性不重要的评估环境。 有关要设置用于配置数据池、计算池和存储池的副本数的环境变量的详细信息，请参阅[部署文档](deployment-guidance.md#configfile)。

- 必须在计算机的 BIOS 中启用 VT-x 或 AMD-v 虚拟化。

## <a name="install-dependencies"></a>安装依赖项

1. 安装 [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)。

1. 安装 Python 3：
   - 如果缺少 pip，请下载 [get-clspip.py](https://bootstrap.pypa.io/get-pip.py) 并运行 `python get-pip.py`。
   - 使用 `python -m pip install requests` 安装 requests 包。

1. 如果还没有安装虚拟机监控程序，请立即安装。
   - 对于 OS X，请安装 [xhyve 驱动程序](https://git.k8s.io/minikube/docs/drivers.md)、[VirtualBox](https://www.virtualbox.org/wiki/Downloads) 或 [VMware Fusion](https://www.vmware.com/products/fusion)。
   - 对于 Linux，请安装 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 或 [KVM](https://www.linux-kvm.org/)。
   - 对于 Windows，请安装 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 或 [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install)。 如果没有在 hyper-v 中配置外部交换机，则创建具有外部网络访问权限的外部交换机。  了解如何[在 hyper-v 中为 minikube 创建外部交换机](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/)。

## <a name="install-minikube"></a>安装 minikube

根据 [v0.28.2 发行版](https://github.com/kubernetes/minikube/releases/tag/v0.28.2)的说明安装 minikube。 SQL Server 2019 大数据群集（预览版）仅适用于 v0.24.1 及更高版本。

## <a name="create-a-minikube-cluster"></a>创建 minikube 群集

以下命令在 Hyper-V VM 中创建具有 8 个 CPU、28 GB 内存和 100 GB 磁盘大小的 minikube 群集。 磁盘大小不是保留空间。  它根据需要在磁盘上增长到该大小。  我们建议不要将磁盘空间更改为小于 100 GB 的数值，因为我们在测试中使用此类配置时遇到了问题。 此命令还显式指定了具有外部访问权限的 hyper-v 交换机。

根据需要更改 **--memory** 等参数，具体取决于可用硬件和使用的虚拟机监控程序。  确保 **--hyper-v** 虚拟交换机参数值与创建虚拟交换机时使用的名称匹配。

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

如果将 minikube 与 VirtualBox 配合使用，命令将如下所示：

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>使用 Hyper-V 禁用自动检查点

在 Windows 10 中，VM 上启用了自动检查点。 在 PowerShell 中执行以下命令，以禁用 VM 上的自动检查点。

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>后续步骤

本文中的步骤配置了 minikube 群集。 下一步是部署 SQL Server 2019 大数据群集。 有关说明，请参阅以下文章：

[在 Kubernetes 上部署 SQL Server 2019 大数据群集](deployment-guidance.md#deploy)
