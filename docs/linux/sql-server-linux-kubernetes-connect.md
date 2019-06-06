---
title: Kubernetes 群集上连接到 SQL Server Always On 可用性组
description: 此文章介绍了如何连接到 Alwayson 可用性组
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1afe2f33ec49f734e97a24a98d62c17b638e38cf
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66713312"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>连接到 SQL Server Alwayson 可用性组在 Kubernetes 上

若要连接到 SQL Server 实例上的 Kubernetes 群集的容器中，创建[负载平衡器服务](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)。 负载均衡器是一个终结点。 它保留的 IP 地址，并将转发到 pod 正在运行的 SQL Server 实例的 IP 地址的请求。

若要连接到可用性组副本，请创建另一副本类型的服务。 您所见的不同类型的副本中的服务示例[sql 的服务器的示例/ag-services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)。

* `ag1-primary` 指向主副本。
* `ag1-secondary` 指向任何辅助副本。

如果有多个辅助副本，Kubernetes 会将你的连接路由到以轮循机制方式的不同副本。

## <a name="create-a-load-balancer-service"></a>创建负载平衡器服务

若要创建的主和副本的负载均衡器服务，请将复制[ `ag1-services.yaml` ](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml)从[sql server 示例](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-file)和更新可用性组。

以下命令将应用从配置`.yaml`到群集的文件：

```kubectl
kubectl apply -f ag1-services.yaml --namespace ag1
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>为负载均衡器服务获取的 IP 地址

若要获取负载均衡器服务的负载均衡器 IP 地址，请运行

```kubectl
kubectl get services
```

标识你想要连接到该服务的 IP 地址。

## <a name="connect-to-primary-replica"></a>连接到主副本

若要连接到 SQL 身份验证的主副本，请使用`sa`帐户、 的值为`sapassword`从所创建的机密和此 IP 地址。

例如：

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>后续步骤

[管理 Kubernetes 群集上的 SQL Server 可用性组](sql-server-linux-kubernetes-manage.md)

[Kubernetes 群集上的 SQL Server 可用性组](sql-server-ag-kubernetes.md)
