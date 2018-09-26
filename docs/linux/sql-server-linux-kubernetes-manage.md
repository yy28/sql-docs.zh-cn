---
title: 管理 SQL Server Always On 可用性组 Kubernetes
description: 本文介绍如何管理 SQL Server Always On 可用性组在 Kubernetes 中。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 078149ff8d9c9c81ac8db95862bf685ca66fbe36
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049347"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>管理 SQL Server Alwayson 可用性组 Kubernetes

若要管理 Always On 可用性组在 Kubernetes 上，创建一个清单，并将其应用到群集。 该清单是`.yaml`文件。  

这篇文章中的示例适用于所有 Kubernetes 群集。 在这些示例方案将应用针对在 Azure Kubernetes 服务群集。

示例，请参阅中的端到端部署[本教程](tutorial-sql-server-ag-kubernetes.md)。

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>故障转移-在 Kubernetes 上的 SQL Server 可用性组

若要故障转移到另一个节点在 Kubernetes 中的可用性组主副本，使用作业。 此项目用于标识此作业的环境变量。

下面的示例清单文件的描述手动故障转移可用性组上的 Kubernetes 副本的作业的作业。 复制到新文件的示例内容`failover.yaml`。

[failover.yaml](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/templates/failover.yaml)

若要部署作业，请使用`Kubectl`。

```azurecli
kubectl apply -f failover.yaml
```

在应用清单文件时，Kubernetes 运行作业。 作业运行时，监督程序选拨一个新领导，并将主副本移动到 SQL Server 实例的领导。

在运行该作业后，请将其删除。 以便您可以查看其状态，完成后将保持在 Kubernetes 中的作业对象。 需要注意的它们的状态后手动删除旧作业。 删除作业也会删除 Kubernetes 日志。 如果你不删除该作业，未来的故障转移作业将失败，除非您更改的作业名称和 pod 选择器。 有关详细信息，请参阅[完成运行作业-](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)。

## <a name="rotate-credentials"></a>滚动更新凭据

旋转更新 SA 和主密钥的凭据。

复制[旋转 creds.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script)本地使用`kubectl`以将其应用到你的群集。

```azurecli
kubectl apply -f rotate-creds.yaml
```

## <a name="next-steps"></a>后续步骤

[访问 Kubernetes 仪表板与 Azure Kubernetes 服务 (AKS)](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Kubernetes 群集上的 SQL Server 可用性组](sql-server-ag-kubernetes.md)