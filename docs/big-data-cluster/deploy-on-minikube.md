---
title: 用于 SQL Server 2019 大数据群集部署配置 Minikube |Microsoft Docs
description: 了解如何为 SQL Server 2019 大数据群集 （预览版） 部署一台计算机上配置 Minikube。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 4a3785d994b6bd40b6b808d07d5272fa7534a7fb
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221564"
---
# <a name="configure-minikube-for-sql-server-2019-big-data-cluster-deployments"></a>Minikube 配置用于 SQL Server 2019 大数据群集部署

本文介绍如何配置**minikube**用于 SQL Server 2019 大数据群集 （预览版） 部署一台计算机上。 Minikube 是一种工具，轻松地在一台便携式计算机或桌面等一台计算机上运行 Kubernetes。 Minikube 在 VM 的单节点 Kubernetes 群集在笔记本电脑上运行的用户希望试用 Kubernetes 或使用它开发日常。 

## <a name="prerequisites"></a>必要條件

- 若要为 SQL Server 2019 CTP 2.1 SQL 大数据群集配置中运行 Minikube 群集，建议你的计算机具有至少 32 GB RAM。

   > [!TIP] 
   > 如果计算机已配置推荐的内存的最小值，然后配置群集，使只有一个计算池实例、 数据池实例 1 和 1 的存储池实例的部署。 此配置应仅用于评估环境的持续性和可用性的数据不重要。 请参阅[部署文档](deployment-guidance.md#define-environment-variables)对于要为配置数据池的副本数设置的环境变量的详细信息，计算池和存储池。

- 必须在计算机的 BIOS 中启用 VT x 或 amd-v 虚拟化。

## <a name="install-dependencies"></a>安装依赖项

1. 如果尚未安装，安装 git 在本地[Windows](https://git-for-windows.github.io/)， [Linux 或 Mac](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。

1. 安装[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)。

1. 安装 Python 3:
   - 如果 pip 是缺失，请下载[get clspip.py](https://bootstrap.pypa.io/get-pip.py)并运行`python get-pip.py`。
   - 安装请求包使用`python -m pip install requests`。

1. 如果你还没有安装在虚拟机监控程序，请立即安装一个。
   - 适用于 OS X 安装[xhyve 驱动程序](https://git.k8s.io/minikube/docs/drivers.md)， [VirtualBox](https://www.virtualbox.org/wiki/Downloads)，或[VMware Fusion](https://www.vmware.com/products/fusion)。
   - 对于 Linux，安装[VirtualBox](https://www.virtualbox.org/wiki/Downloads)或[KVM](http://www.linux-kvm.org/)。
   - 对于 Windows，安装[VirtualBox](https://www.virtualbox.org/wiki/Downloads)或[HYPER-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install)。 如果没有外部交换机的 hyper-v 中配置，然后创建一个具有外部网络访问权限。  请参阅如何[minikube 的 hyper-v 中创建外部交换机](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/)。

## <a name="install-minikube"></a>安装 Minikube

根据说明安装 Minikube [v0.28.2 版本](https://github.com/kubernetes/minikube/releases/tag/v0.28.2)。 SQL Server 2019 CTP 2.1 大数据群集仅适用于版本 v0.24.1 和设置。

## <a name="create-a-minikube-cluster"></a>创建 Minikube 群集

下面的命令中的 HYPER-V VM 具有 8 个 Cpu，28 GB 内存，并为 100 GB 的磁盘大小创建 minikube 群集。 磁盘大小不是保留的空间。  它可增长到该大小在磁盘上根据需要。  我们建议不更改磁盘空间为我们遇到了问题，在测试中小于 100 GB。 这还将指定的 hyper-v 交换机与外部访问显式。

更改参数，如 **-内存**根据需要根据可用的硬件和其正在使用的虚拟机监控程序。  请确保 **-hyper v**虚拟交换机参数值与创建你的虚拟交换机时使用的名称匹配。

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

如果使用 VirtualBox 使用 Minikube 该命令将如下所示：

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>禁用 hyper-v 自动检查点

Windows 10 上的 VM 上启用了自动检查点。 若要禁用自动检查点在 VM 上的 PowerShell 中执行以下命令。

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>后续步骤

在本文中的步骤配置 Minikube 群集。 下一步是部署 SQL Server 2019 大数据群集。 有关说明，请参阅以下文章：

[部署 Kubernetes 上的 SQL Server 2019 CTP 2.1](deployment-guidance.md#deploy)
