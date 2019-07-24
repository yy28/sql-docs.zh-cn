---
title: 什么是应用程序部署？
titleSuffix: SQL Server 2019 big data clusters
description: 本文介绍 SQL Server 2019 大数据群集 (预览版) 上的应用程序部署。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d8cc44862af21c54bdbd0e4adbb35db912c3f7c9
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419404"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>什么是 SQL Server 2019 大数据群集上的应用程序部署？

使用应用程序部署, 可以通过提供用于创建、管理和运行应用程序的接口, 来部署大数据群集上的应用程序。 部署在大数据群集上的应用程序可以受益于群集的计算能力, 并可以访问群集上可用的数据。 这会提高应用程序的可伸缩性和性能, 同时管理数据所在的应用程序。
以下部分介绍应用程序部署的体系结构和功能。

## <a name="application-deployment-architecture"></a>应用程序部署体系结构

应用程序部署由控制器和应用运行时处理程序组成。 创建应用程序时, 将提供规范文件`spec.yaml`()。 此`spec.yaml`文件包含控制器成功部署应用程序所需要了解的所有内容。 下面是以下内容`spec.yaml`的示例:

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

控制器将检查`spec.yaml`文件`runtime`中指定的, 并调用相应的运行时处理程序。 运行时处理程序将创建该应用程序。 首先, 创建一个包含一个或多个 pod 的 Kubernetes ReplicaSet, 其中每个 pod 都包含要部署的应用程序。 Pod 的数目由`replicas`应用程序`spec.yaml`文件中的参数集定义。 每个 pod 可以有一个或多个池。 池的数目由`poolsize` `spec.yaml`文件中的参数集定义。

这些设置会影响部署可并行处理的请求数量。 一次给定时间内的最大请求数是等于`replicas`。 `poolsize` 如果每个副本有5个副本和2个池, 则部署可以并行处理10个请求。 请参阅下图, 了解`replicas`和`poolsize`的图形化表示形式:

![Poolsize 和副本](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

创建 ReplicaSet 并启动 pod 后, 如果`schedule` `spec.yaml`在文件中设置了, 则将创建一个 cron 作业。 最后, 创建可用于管理和运行应用程序的 Kubernetes 服务 (请参阅下文)。

执行应用程序时, 应用程序的 Kubernetes 服务会将请求发送到副本并返回结果。

## <a name="how-to-work-with-application-deployment"></a>如何使用应用程序部署

应用程序部署的两个主要接口是: 
- [命令行接口`azdata`](big-data-cluster-create-apps.md)
- [Visual Studio Code 和 Azure Data Studio 扩展](app-deployment-extension.md)

还可以使用 RESTful web 服务来执行应用程序。 有关详细信息, 请参阅对[大数据群集使用应用程序](big-data-cluster-consume-apps.md)。

## <a name="next-steps"></a>后续步骤

若要详细了解如何在 SQL Server 大数据群集上创建和运行应用程序, 请参阅以下内容:

- [使用 azdata 部署应用程序](big-data-cluster-create-apps.md)
- [使用应用部署扩展部署应用程序](app-deployment-extension.md)
- [使用大数据群集上的应用程序](big-data-cluster-consume-apps.md)

若要详细了解 SQL Server 大数据群集, 请参阅以下概述:

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
