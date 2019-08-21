---
title: 入门
titleSuffix: SQL Server big data clusters
description: 了解部署[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (预览版) 的步骤和资源。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 323394f9590551528ce9e9dfdf1fb97c7d1c2225
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653395"
---
# <a name="get-started-with-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>入门[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文提供了有关如何部署[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)的概述。 其旨在使用户熟悉概念并提供用于理解本部分中其他部署文章的框架。 具体部署步骤因客户端和服务器的平台选择而异。

> [!TIP]
> 若要快速获取一个环境, 使其部署了 Kubernetes 和大数据群集, 以帮助你提升其功能, 请使用[脚本部分](#scripts)中指向的示例脚本之一。 部署后, 若要管理群集, 请使用以下部分中的[客户端工具](#tools)。

## <a id="tools"></a> 客户端工具

大数据群集需要一组特定的客户端工具。 将大数据群集部署到 Kubernetes 之前，应安装以下工具：

| Tool | 描述 |
|---|---|
| **azdata** | 部署和管理大数据群集。 |
| **kubectl** | 创建和管理基础 Kubernetes 群集。 |
| **Azure Data Studio** | 使用大数据群集的图形界面。 |
| **SQL Server 2019 扩展** | 启用大数据群集功能的 Azure Data Studio 扩展。 |

对于不同方案，需要使用其他工具。 每篇文章都应说明用于执行特定任务的必需工具。 有关工具和安装链接的完整列表，请参阅[安装 SQL Server 2019 大数据工具](deploy-big-data-tools.md)。

## <a name="kubernetes"></a>Kubernetes

大数据群集被部署为在 [Kubernetes](https://kubernetes.io/docs/home) 中进行管理的一系列相关容器。 可通过多种方式托管 Kubernetes。 即使已有现有的 Kubernetes 环境，也应查看大数据群集的相关要求。

- **Azure Kubernetes 服务 (AKS)** ：AKS 支持在 Azure 中部署托管的 Kubernetes 群集。 用户仅管理和维护代理节点。 使用 AKS，无需为群集预配硬件。 还可轻松使用 [python 脚本](quickstart-big-data-cluster-deploy.md)或[部署笔记本](deploy-notebooks.md)创建 AKS 群集和部署大数据群集，只需一步即可完成。 有关为大数据群集部署配置 AKS 的详细信息, 请参阅为[ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]部署配置 Azure Kubernetes 服务](deploy-on-aks.md)。

- **多台计算机**：还可以将 Kubernetes 部署到多台 Linux 计算机，这些计算机可以是物理服务器或虚拟机。 可使用 [Kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) 工具创建 Kubernetes 群集。 可使用 [bash 脚本](deployment-script-single-node-kubeadm.md)自动执行此类部署。 如果已有想要用于大数据群集的现有基础结构，此方法会很有效。 有关将**kubeadm**部署用于大数据群集的详细信息, 请参阅[在多台计算机上[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]配置 Kubernetes 以进行部署](deploy-with-kubeadm.md)。

- **Minikube**：Minikube 支持在单个服务器上本地运行 Kubernetes。 如果正在试用大数据群集，或者需要在测试或开发方案中使用它，不妨选择此工具。 有关使用 Minikube 的详细信息，请参阅 [Minikube 文档](https://kubernetes.io/docs/setup/minikube/)。 有关将 Minikube 与大数据群集配合使用的具体要求，请参阅[为 SQL Server 2019 大数据群集部署配置 minikube](deploy-on-minikube.md)。

## <a name="deploy-a-big-data-cluster"></a>部署大数据群集

配置 Kubernetes 后，可使用 `azdata bdc create` 命令部署大数据群集。 部署时，可采用多种不同的方法。

- 若要部署到开发测试环境，则可选择使用 azdata 提供的[默认配置](deployment-guidance.md#deploy)之一。

- 若要自定义部署，可以创建并使用自己的[部署配置文件](deployment-guidance.md#configfile)。

- 对于完全无人参与的安装，可以传递环境变量中的所有其他设置。 有关详细信息，请参阅[无人参与的部署](deployment-guidance.md#unattended)。


## <a id="scripts"></a>部署脚本

通过部署脚本，只需一个步骤即可部署 Kubernetes 和大数据群集。 部署脚本还经常为大数据群集设置提供默认值。 可以通过创建自己的版本来自定义任何部署脚本，以便以不同的方式配置大数据群集部署。

以下部署脚本当前可用：

- [Python 脚本 - 部署 Azure Kubernetes 服务 (AKS) 上的大数据群集](quickstart-big-data-cluster-deploy.md)
- [Bash 脚本 - 将大数据群集部署到单个节点 kubeadm 群集](deployment-script-single-node-kubeadm.md)

## <a name="deployment-notebooks"></a>部署笔记本

还可以通过运行 Azure Data Studio 笔记本部署大数据群集。 有关如何在 AKS 上使用笔记本进行部署的详细信息，请参阅以下文章：

- [使用 Azure Data Studio 笔记本部署大数据群集](deploy-notebooks.md)。

## <a name="next-steps"></a>后续步骤

成功部署大数据群集后，[连接到该群集](connect-to-big-data-cluster.md)并考虑[加载示例数据](tutorial-load-sample-data.md)以便与多个演练配合使用。
