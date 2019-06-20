---
title: 什么是应用程序部署？
titleSuffix: SQL Server 2019 big data clusters
description: 本文介绍如何在 SQL Server 2019 大数据群集 （预览版） 上的应用程序部署。
author: jterh
ms.author: jroth
manager: jroth
ms.date: 03/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1a6ba9caed2b01abc50e16e34d1a13413af2d0ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801858"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>什么是 SQL Server 2019 大数据群集上的应用程序部署？

应用程序部署通过提供接口以创建、 管理和运行应用程序，大数据群集上的应用程序的部署。 大数据群集上部署的应用程序受益于群集的计算能力，并且可以访问可在群集的数据。 这会增加可伸缩性和性能的应用程序，同时管理数据所在的应用程序。
以下部分介绍的体系结构和应用程序部署功能。

## <a name="application-deployment-architecture"></a>应用程序部署体系结构

应用程序部署由一个控制器和应用程序运行时处理程序组成。 如果创建的应用，规范文件 (`spec.yaml`) 提供。 这`spec.yaml`文件包含在控制器需要知道要成功部署应用程序的所有内容。 以下是有关内容的示例`spec.yaml`:

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

控制器会检查`runtime`中指定`spec.yaml`文件，并调用相应的运行时处理程序。 运行时处理程序创建应用程序。 首先，Kubernetes 副本集将创建包含一个或多个 pod，其中每个包含要部署的应用程序。 由定义的 pod 数`replicas`参数中设置`spec.yaml`应用程序文件。 每个 pod 可以有一个更多池。 定义池的数量`poolsize`参数中设置`spec.yaml`文件。

这些设置会影响部署可以并行处理的请求量。 在一个给定时间的请求最大数目是等于`replicas`时间`poolsize`。 如果你有 5 个副本和 2 个池每个副本部署可以处理 10 个并行请求。 请参阅下的图以图形表示形式`replicas`和`poolsize`:

![Poolsize 和副本](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

如果已创建的副本集，并且已启动 pod 后，创建一个 cron 作业`schedule`已设置在`spec.yaml`文件。 最后，Kubernetes 创建一个服务，可用于管理和运行应用程序 （见下文）。

执行应用程序时，应用程序代理将请求发送到副本并将结果返回的 Kubernetes 服务。

## <a name="how-to-work-with-application-deployment"></a>如何使用应用程序部署

应用程序部署的两个主要接口是： 
- [命令行接口 `mssqlctl`](big-data-cluster-create-apps.md)
- [Visual Studio Code 和 Azure Data Studio 扩展](app-deployment-extension.md)

还有可能要执行使用 RESTful web 服务的应用程序。 有关详细信息，请参阅[使用大数据群集上的应用程序](big-data-cluster-consume-apps.md)。

## <a name="next-steps"></a>后续步骤

若要了解有关如何创建和 SQL Server 大数据群集上运行的应用程序的详细信息，请参阅以下：

- [使用 mssqlctl 部署应用程序](big-data-cluster-create-apps.md)
- [部署应用程序使用应用程序部署扩展](app-deployment-extension.md)
- [使用大数据群集上的应用程序](big-data-cluster-consume-apps.md)

若要了解有关 SQL Server 大数据群集的详细信息，请参阅以下概述：

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
