---
title: 入门
titleSuffix: SQL Server big data clusters
description: 了解步骤以及用于部署 SQL Server 2019 大数据群集 （预览版） 的资源。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b090ec57ae62058a211e4e232f8bfa99e44f9675
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728955"
---
# <a name="get-started-with-sql-server-big-data-clusters"></a>SQL Server 大数据群集入门

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文概述了如何部署[SQL Server 2019 大数据群集 （预览版）](big-data-cluster-overview.md)。 它旨在面向您的概念并提供一个框架，用于了解在本部分中的其他部署文章。 根据您为客户端和服务器的平台选择具体的部署步骤可能有所不同。

## <a id="tools"></a> 客户端工具

大数据群集需要一组特定的客户端工具。 大数据群集部署到 Kubernetes 之前，应安装以下工具：

| Tool | 描述 |
|---|---|
| **mssqlctl** | 部署和管理大数据群集。 |
| **kubectl** | 创建和管理基础的 Kubernetes 群集。 |
| **Azure Data Studio** | 使用大数据群集的图形界面。 |
| **SQL Server 2019 扩展** | Azure Data Studio 扩展使大数据群集功能。 |

其他工具所需的不同方案。 每个项目应解释为执行特定任务的必备工具。 有关工具和安装链接的完整列表，请参阅[安装 SQL Server 2019 大数据工具](deploy-big-data-tools.md)。

## <a name="kubernetes"></a>Kubernetes

作为一系列相互关联中托管的容器部署大数据群集[Kubernetes](https://kubernetes.io/docs/home)。 你可以托管在不同的方式中的 Kubernetes。 即使你已有现有的 Kubernetes 环境，应查看大数据群集的相关的要求。

- **Azure Kubernetes 服务 (AKS)** :AKS，可部署在 Azure 中托管的 Kubernetes 群集。 只能管理和维护的代理节点。 通过 AKS，您无需预配群集的硬件。 它也很容易使用大数据群集[部署脚本](quickstart-big-data-cluster-deploy.md)创建 AKS 群集和部署大数据群集在一个步骤中的。 有关将 AKS 用于大数据群集的详细信息，请参阅[用于 SQL Server 2019 大数据群集 （预览版） 部署中配置 Azure Kubernetes 服务](deploy-on-aks.md)。

- **多台计算机**:此外可以将 Kubernetes 部署到多台 Linux 计算机，可以是物理服务器或虚拟机。 [Kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/)工具可用来创建 Kubernetes 群集。 如果已有想要用于大数据群集的现有基础结构，此方法适用。 有关使用详细信息**kubeadm**部署大数据群集，请参阅[配置用于 SQL Server 2019 大数据群集 （预览版） 部署多台计算机上的 Kubernetes](deploy-with-kubeadm.md)。

- **Minikube**:Minikube，可在单个服务器上本地运行 Kubernetes。 如果您尝试大数据群集或需要在测试或开发方案中使用它，它是一个不错的选择。 有关使用 Minikube 的详细信息，请参阅[Minikube 文档](https://kubernetes.io/docs/setup/minikube/)。 有关在使用 Minikube 的大数据群集的特定要求，请参阅[配置用于 SQL Server 2019 大数据群集部署 minikube](deploy-on-minikube.md)。

## <a name="deploy-a-big-data-cluster"></a>部署大数据群集

配置 Kubernetes 之后, 你部署使用的大数据群集`mssqlctl bdc create`命令。 在部署时，您可以采取几种不同方法。

- 如果您要部署到开发测试环境，你可以选择使用之一[默认配置](deployment-guidance.md#deploy)提供**mssqlctl**。

- 若要自定义部署，可以创建并使用您自己[部署配置文件](deployment-guidance.md#configfile)。

- 对于完全无人参与安装，可以在环境变量中传递的所有其他设置。 有关详细信息，请参阅[无人参与的部署](deployment-guidance.md#unattended)。

## <a name="deployment-scripts"></a>部署脚本

部署脚本可以帮助部署 Kubernetes 和大数据群集中单个步骤。 它们通常还为大数据群集设置提供默认值。 大数据群集在 Azure Kubernetes 服务 (AKS) 的部署脚本的示例，请参阅以下文章：

[部署大数据使用部署脚本 (AKS) 群集 SQL Server 2019](quickstart-big-data-cluster-deploy.md)。

通过创建自己的版本，用于以不同的方式配置大数据群集环境变量，可以自定义任何部署脚本。

## <a name="next-steps"></a>后续步骤

已成功部署大数据群集后[连接到群集](connect-to-big-data-cluster.md)，并考虑[加载示例数据](tutorial-load-sample-data.md)用于一些演练。