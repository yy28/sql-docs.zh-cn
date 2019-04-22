---
title: 入门
titleSuffix: SQL Server big data clusters
description: 了解步骤以及用于部署 SQL Server 2019 大数据群集 （预览版） 的资源。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 69b5d9b69536243d371cb45c1c46620f5194657d
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860428"
---
# <a name="get-started-with-sql-server-big-data-clusters"></a>SQL Server 大数据群集入门

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文概述了如何部署[SQL Server 2019 大数据群集 （预览版）](big-data-cluster-overview.md)。 它旨在面向您的概念并提供一个框架，用于了解在本部分中的其他部署文章。 根据您为客户端和服务器的平台选择具体的部署步骤可能有所不同。

## <a id="tools"></a> 客户端工具

大数据群集需要一组特定的客户端工具。 大数据群集部署到 Kubernetes 之前，应安装以下工具：

| Tool | Description |
|---|---|
| **mssqlctl** | 部署和管理大数据群集。 |
| **kubectl** | 创建和管理基础的 Kubernetes 群集。 |
| **Azure Data Studio** | 使用大数据群集的图形界面。 |
| **SQL Server 2019 扩展** | Azure Data Studio 扩展使大数据群集功能。 |

其他工具所需的不同方案。 每个项目应解释为执行特定任务的必备工具。 有关工具和安装链接的完整列表，请参阅[安装 SQL Server 2019 大数据工具](deploy-big-data-tools.md)。

## <a name="kubernetes"></a>Kubernetes

作为一系列相互关联中托管的容器部署大数据群集[Kubernetes](https://kubernetes.io/docs/home)。 你可以托管在不同的方式中的 Kubernetes。 即使你已有现有的 Kubernetes 环境，应查看大数据群集的相关的要求。

- **Azure Kubernetes 服务 (AKS)**:AKS，可部署在 Azure 中托管的 Kubernetes 群集。 只能管理和维护的代理节点。 通过 AKS，您无需预配群集的硬件。 它也很容易使用大数据群集[部署脚本](quickstart-big-data-cluster-deploy.md)创建 AKS 群集和部署大数据群集在一个步骤中的。 有关将 AKS 用于大数据群集的详细信息，请参阅[用于 SQL Server 2019 大数据群集 （预览版） 部署中配置 Azure Kubernetes 服务](deploy-on-aks.md)。

- **多台计算机**:此外可以将 Kubernetes 部署到多台 Linux 计算机，可以是物理服务器或虚拟机。 [Kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/)工具可用来创建 Kubernetes 群集。 如果已有想要用于大数据群集的现有基础结构，此方法适用。 有关使用详细信息**kubeadm**部署大数据群集，请参阅[配置用于 SQL Server 2019 大数据群集 （预览版） 部署多台计算机上的 Kubernetes](deploy-with-kubeadm.md)。

- **Minikube**:Minikube，可在单个服务器上本地运行 Kubernetes。 如果您尝试大数据群集或需要在测试或开发方案中使用它，它是一个不错的选择。 有关使用 Minikube 的详细信息，请参阅[Minikube 文档](https://kubernetes.io/docs/setup/minikube/)。 有关在使用 Minikube 的大数据群集的特定要求，请参阅[配置用于 SQL Server 2019 大数据群集部署 minikube](deploy-on-minikube.md)。

## <a name="deployment-scripts"></a>部署脚本

部署脚本可以帮助部署 Kubernetes 和大数据群集中单个步骤。 它们通常还为必需的环境变量提供默认值。 大数据群集在 Azure Kubernetes 服务 (AKS) 的部署脚本的示例，请参阅[部署大数据使用部署脚本 (AKS) 群集 SQL Server 2019](quickstart-big-data-cluster-deploy.md)。

通过创建自己的版本，用于以不同的方式配置大数据群集环境变量，可以自定义任何部署脚本。

## <a name="deploy-a-big-data-cluster"></a>部署大数据群集

若要将 Kubernetes 和大数据群集到 AKS 部署与单个脚本，请参阅下面的示例：

- [部署 SQL Server 2019 大数据群集使用部署脚本 (AKS)](quickstart-big-data-cluster-deploy.md)

有关部署使用 AKS、 kubeadm 和 MiniKube 的大数据群集的详细的部署指南，请参阅以下文章：

- [如何部署 SQL Server 大数据群集在 Kubernetes 上](deployment-guidance.md)

## <a name="next-steps"></a>后续步骤

已成功部署大数据群集后[连接到群集](connect-to-big-data-cluster.md)，并考虑[加载示例数据](tutorial-load-sample-data.md)用于一些演练。