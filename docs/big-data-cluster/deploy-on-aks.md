---
title: 配置用于 SQL Server 2019 大数据群集部署的 Azure Kubernetes 服务 |Microsoft Docs
description: 了解如何配置用于 SQL Server 2019 大数据群集 （预览版） 部署的 Azure Kubernetes 服务 (AKS)。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 0eda19b4a241a066771afff1cfb682fa7234f81e
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51700380"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-2019-preview-deployments"></a>为 SQL Server 2019 （预览版） 部署配置 Azure Kubernetes 服务

本文介绍如何配置用于 SQL Server 2019 大数据群集 （预览版） 部署的 Azure Kubernetes 服务 (AKS)。 

AKS 轻松创建、 配置和管理 Kubernetes 群集以运行容器化应用程序使用的预配置的虚拟机群集。 这使您可以使用现有技能或大量不断增长的社区专业知识，在部署和管理基于容器的 Microsoft Azure 上的应用程序。

本文介绍部署 Kubernetes AKS 使用 Azure CLI 上的步骤。 如果还没有 Azure 订阅，请在开始之前创建一个免费帐户。

> [!TIP] 
> 部署 AKS 和 SQL Server 大数据群集的示例 python 脚本，请参阅[部署大数据群集在 Azure Kubernetes 服务 (AKS) SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks)。

## <a name="prerequisites"></a>必要條件

- 对于 AKS 环境中，以获得最佳体验时验证的基本方案，我们建议使用至少 4 个 Vcpu 和 32 GB 的内存每个虚拟机 （除了 master)，至少三个代理。 Azure 基础结构提供了多个 Vm 的大小选项，请参阅[此处](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)为计划部署的目标区域中的选择。
  
- 此部分要求，必须运行 Azure CLI 2.0.4 或更高版本。 如果你需要安装或升级，请参阅[安装 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。 运行`az --version`如果需要查找版本。

- 安装[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)版本 1.10 的最少。 如果你想要 kubectl 客户端上安装特定版本，请参阅[安装 kubectl 二进制通过 curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl)。 

- 同一 1.10 最低版本适用于 Kubernetes 服务器。 适用于 AKS，您需要使用`--kubernetes-version`参数来指定默认值以外的版本。

> [!NOTE]
请注意，客户端/服务器版本，它是倾斜支持为 + /-1 的次要版本。 Kubernetes 文档指出，"客户端应是偏斜的多个次要版本，从主服务器，但可能会导致的最多为 1 个次要版本 master。 例如，v1.3 master 应适用于 v1.1 和 v1.2，v1.3 节点和应使用 v1.2、 v1.3 和 v1.4 客户端。" 有关详细信息，请参阅[Kubernetes 支持的版本和组件倾斜](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)。

另请注意，`az aks kubernetes install-cli`将安装 kubectl 客户端版本较低的所需的 1.10。 按照上述说明安装 kubectl 客户端的正确版本。

## <a name="create-a-resource-group"></a>创建资源组

Azure 资源组是在哪个 Azure 中部署和管理资源的逻辑组。 以下步骤登录到 Azure 并创建 AKS 群集的资源组。

> [!TIP]
> 如果使用的 Windows，使用 PowerShell 步骤的其余部分。

1. 在命令提示符处，运行以下命令并按照提示登录到 Azure 订阅：

    ```bash
    az login
    ```

1. 如果有多个订阅可以通过运行以下命令来查看所有订阅：

   ```bash
   az account list
   ```

1. 如果你想要将更改为不同的订阅可以运行以下命令：

   ```bash
   az account set --subscription <subscription id>
   ```

1. 创建一个包含资源组**az 组创建**命令。 下面的示例创建名为的资源组`sqlbigdatagroup`在`westus2`位置。

   ```bash
   az group create --name sqlbigdatagroup --location westus2
   ```

## <a name="create-a-kubernetes-cluster"></a>创建 Kubernetes 群集

1. 在与 AKS 创建 Kubernetes 群集[az aks 创建](https://docs.microsoft.com/cli/azure/aks)命令。 下面的示例创建名为的 Kubernetes 群集*kubcluster*包含一个 Linux 主节点和两个 Linux 代理节点。 请确保你在前面几节中使用同一资源组中创建 AKS 群集。

    ```bash
   az aks create --name kubcluster \
    --resource-group sqlbigdatagroup \
    --generate-ssh-keys \
    --node-vm-size Standard_E4s_v3 \
    --node-count 3 \
    --kubernetes-version 1.10.8
    ```

    可以增加或减少 Kubernetes 代理节点数，方法是更改`--node-count <n>`其中`<n>`是数字的你想要具有代理节点，它不包括主 Kubernetes 节点。 因此在上面的示例中，将有**4** Vm 的大小**Standard_E4s_v3**用于 AKS 群集： **1**的 master 和**3**为代理节点。

    几分钟后，该命令完成并返回有关群集的 JSON 格式信息。

1. 保存 JSON 输出以供将来使用前一命令。

## <a name="connect-to-the-cluster"></a>连接到群集

1. 若要配置 kubectl 以连接到 Kubernetes 群集，运行[az aks get-credentials 来获取凭据](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials)命令。 此步骤下载凭据，并配置 kubectl CLI 来使用它们。

   ```bash
   az aks get-credentials --resource-group=sqlbigdatagroup --name kubcluster
   ```

1. 若要验证连接到群集，请使用[kubectl 获取](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)命令返回群集节点的列表。  下面的示例中显示的输出如你打算有个主节点和 3 个代理节点。

   ```bash
   kubectl get nodes
   ```

## <a name="next-steps"></a>后续步骤

在本文中的步骤配置在 AKS 中的 Kubernetes 群集。 下一步是将 SQL Server 2019 大数据部署到群集。

[快速入门： 部署 SQL Server 大数据群集在 Azure Kubernetes 服务 (AKS)](quickstart-big-data-cluster-deploy.md)
