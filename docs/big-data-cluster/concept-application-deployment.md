---
title: 什么是应用程序部署？
titleSuffix: SQL Server Big Data Clusters
description: 本文介绍 SQL Server 2019 大数据群集上的应用程序部署。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4b647ab4d03d110ce303388a8b62461f28033b6c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "76831571"
---
# <a name="what-is-application-deployment-on-a-big-data-cluster"></a>什么是大数据群集上的应用程序部署？

应用程序部署通过提供用于创建、管理和运行应用程序的界面，允许在大数据群集上部署应用程序。 部署在大数据群集上的应用程序可以受益于群集的计算能力，并且可以访问群集上可用的数据。 这会提高应用程序的可伸缩性和性能，同时管理数据所在的应用程序。 SQL Server 大数据群集上支持的应用程序运行时包括 R、Python、SSIS、MLeap。

以下部分介绍了应用程序部署的体系结构和功能。

## <a name="application-deployment-architecture"></a>应用程序部署体系结构

应用程序部署由控制器和应用运行时处理程序组成。 创建应用程序时，会提供规范文件 (`spec.yaml`)。 此 `spec.yaml` 文件包含控制器成功部署应用程序所需知道的一切。 下面是 `spec.yaml` 的内容示例：

```yaml
#spec.yaml
name: add-app #name of your python script
version: v1  #version of the app
runtime: Python #the language this app uses (R or Python)
src: ./add.py #full path to the location of the app
entrypoint: add #the function that will be called upon execution
replicas: 1  #number of replicas needed
poolsize: 1  #the pool size that you need your app to scale
inputs:  #input parameters that the app expects and the type
  x: int
  y: int
output: #output parameter the app expects and the type
  result: int
```

控制器会检查 `spec.yaml` 文件中指定的 `runtime`，并调用相应的运行时处理程序。 运行时处理程序会创建应用程序。 首先，会创建包含一个或多个 pod 的 Kubernetes ReplicaSet，其中每个 pod 都包含要部署的应用程序。 pod 的数量由应用程序的 `spec.yaml` 文件中设置的 `replicas` 参数定义。 每个 pod 可以有一个或多个池。 池的数量由 `spec.yaml` 文件中设置的 `poolsize` 参数定义。

这些设置会影响部署可以并行处理的请求数量。 一个给定时间的最大请求数等于 `replicas` 乘以 `poolsize`。 如果有 5 个副本，每个副本有 2 个池，则部署可以并行处理 10 个请求。 有关 `replicas` 和 `poolsize` 的图形表示方式，请参阅下图：

![池大小和副本](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

如果在 `spec.yaml` 文件中设置了 `schedule`，那么，在创建 ReplicaSet 并启动 pod 后，会创建一个 cron 作业。 最后，会创建一个可用于管理和运行应用程序的 Kubernetes 服务（请参阅下文）。

执行应用程序时，应用程序的 Kubernetes 服务会将请求代理给副本并返回结果。

## <a name="how-to-work-with-application-deployment"></a>如何使用应用程序部署

应用程序部署的两个主要接口如下： 
- [命令行接口 `azdata`](big-data-cluster-create-apps.md)
- [Visual Studio Code 和 Azure Data Studio 扩展](app-deployment-extension.md)

还可以使用 RESTful Web 服务执行应用程序。 有关详细信息，请参阅[在大数据群集上使用应用程序](big-data-cluster-consume-apps.md)。

## <a name="next-steps"></a>后续步骤

若要了解有关如何在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 上创建和运行应用程序的详细信息，请参阅以下内容：

- [使用 azdate 部署应用程序](big-data-cluster-create-apps.md)
- [使用应用部署扩展部署应用程序](app-deployment-extension.md)
- [在大数据群集上使用应用程序](big-data-cluster-consume-apps.md)

若要了解有关 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的详细信息，请参阅以下概述：

- [什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
