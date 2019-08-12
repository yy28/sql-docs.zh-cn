---
title: 连接到 Kubernetes 群集上的 SQL Server Always On 可用性组
description: 本文介绍如何连接到 Always On 可用性组
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f05bc51f587723414d3b0a4090fe2b27ad5fb837
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952606"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>连接到 Kubernetes 上的 SQL Server Always On 可用性组

要连接到 Kubernetes 群集上容器中的 SQL Server 实例，请创建[负载均衡器服务](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)。 负载均衡器是一个终结点。 它保留 IP 地址，并将 IP 地址的请求转发到运行 SQL Server 实例的 Pod。

要连接到可用性组副本，请为不同的副本类型创建服务。 可以在 [sql-server-samples/ag-services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) 中看到不同类型的副本的服务示例。

* `ag1-primary` 指向主要副本。
* `ag1-secondary` 指向任何次要副本。

如果有多个次要副本，则 Kubernetes 会以循环方式将连接路由到不同副本。

## <a name="create-a-load-balancer-service"></a>创建负载均衡器服务

要为主要副本和副本创建负载均衡器服务，请从 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-file) 复制 [`ag1-services.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) 并为可用性组更新它。

以下命令将 `.yaml` 文件中的配置应用到群集：

```kubectl
kubectl apply -f ag1-services.yaml --namespace ag1
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>获取负载均衡器服务的 IP 地址

要获取负载均衡器服务的负载均衡器 IP 地址，请运行

```kubectl
kubectl get services
```

确定要连接到的服务的 IP 地址。

## <a name="connect-to-primary-replica"></a>连接到主要副本

要使用 SQL 身份验证连接到主要副本，请使用 `sa` 帐户、所创建的机密中的 `sapassword` 值和此 IP 地址。

例如：

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>后续步骤

[管理 Kubernetes 群集上的 SQL Server 可用性组](sql-server-linux-kubernetes-manage.md)

[Kubernetes 群集上的 SQL Server 可用性组](sql-server-ag-kubernetes.md)
