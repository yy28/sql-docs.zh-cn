---
title: 管理 SQL Server Always On 可用性组 Kubernetes
description: 本文介绍如何在 Kubernetes 中管理 SQL Server Always On 可用性组。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 893e502c35ae33ce6ff87efd88049db97a40f875
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952545"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>管理 SQL Server Always On 可用性组 Kubernetes

若要在 Kubernetes 上管理 Always On 可用性组，请创建清单并将其应用到群集。 该清单是 `.yaml` 文件。  

本文中的示例应用于所有 Kubernetes 群集。 示例中的方案应用于 Azure Kubernetes 服务中的群集。

请参阅[在 Kubernetes 群集上部署 SQL Server Always On 可用性组](sql-server-linux-kubernetes-deploy.md)中的完整部署示例。

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>故障转移 - Kubernetes 上的 SQL Server 可用性组

若要将主副本故障转移或移动到可用性组中的其他节点上，请完成以下步骤：

1. 在清单文件中定义作业。

  [`failover.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/failover.yaml)（位于 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) GitHub 存储库中）介绍了故障转移作业。

  将清单文件复制到管理终端。

  更新环境的文件。

  - 将 `<containerName>` 替换为预期的可用性组目标的 Pod 名称（例如 mssql2-0）。
  - 如果可用性组不在 `ag1` 命名空间中，请将 `ag1` 替换为命名空间。

  此文件定义名为 `manual-failover` 的故障转移作业。

1. 若要部署作业，请使用 `kubectl apply`。 以下脚本将部署作业。

  ```azurecli
  kubectl apply -f failover.yaml
  ```

  部署作业完成后，具有 SQL Server 运算符的 Kubernetes 会执行以下任务：
  
  - 将主副本降级为次要副本
  
  - 将指定副本提升为主副本
  
  应用清单文件后，Kubernetes 会运行该作业。 该作业可以让主管选择新的负责人，并将主副本移到负责人的 SQL Server 实例中。

1. 验证作业是否已完成。
  
  Kubernetes 运行作业之后，可以查看日志。
  
  以下示例返回名为 `manual-failover` 的作业状态。

  ```azurecli
  kubectl describe jobs/manual-failover --namespace ag1
  ```

1. 删除手动故障转移作业。 

  >[!IMPORTANT]
  >必须先手动删除该作业，才能再发出另一手动故障转移。
  > 
  >完成操作后，Kubernetes 中的作业对象会保留下来，以便查看其状态。 记录下旧作业的状态之后，需要手动删除旧作业。 删除作业的同时会删除 Kubernetes 日志。 只有删除作业，将来才能进行故障转移作业（除非更改作业名称和 Pod 选择器）。 有关详细信息，请参阅[作业 - 运行到完成](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)。

  以下命令可删除作业。

  ```azurecli
  kubectl delete jobs manual-failover --namespace ag1
  ```

## <a name="rotate-credentials"></a>轮换凭据

轮换凭据以重置 SQL Server `sa` 帐户和 SQL Server [服务主密钥](../relational-databases/security/encryption/service-master-key.md)的密码。 

为完成此任务，需要在 Kubernetes 群集中创建新的机密，然后创建轮换凭据的作业。

在轮换凭据之前，请为密码和主密钥创建新的机密。

以下脚本创建名为 `new-sql-secrets` 的机密。 在运行脚本之前，请将 `<>` 替换为 `sapassword` 和 `masterkeypassword` 的复杂密码。 对每个值使用不同的密码。

```azurecli
kubectl create secret generic new-sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
```

对需要主密钥或 `sa` 密码的每个 SQL Server 实例完成以下步骤。

1. 将 [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) 复制到管理终端。

  [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml)（位于 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/) GitHub 存储库中）是该作业的清单示例。

  在应用此清单之前，请更新环境的清单。 根据需要查看和更改以下设置。

  - 验证命名空间。 必要时进行更新。 清单中的以下示例应用于名为 `ag1` 的命名空间。

    ```yaml
    metadata:
      name: rotate-creds
      namespace: ag1
    ```

  - 验证 SQL Server 实例的名称。 必要时进行更新。 清单规范中的以下示例应用于名为 `mssql1` 的 SQL Server 实例。

    ```yaml
    env:
      - name: MSSQL_K8S_SQL_SERVER_NAME
        value: mssql1
    ```

  将更新的清单文件保存到工作站。

1. 请使用 `kubectl` 部署作业。

  ```azurecli
  kubectl apply -f rotate-creds.yaml --namespace ag1
  ```

  Kubernetes 为可用性组中的一个 SQL Server 实例更新主密钥和 `sa` 密码。

1. 验证作业是否已完成。 运行以下命令：为验证作业是否已完成，请运行 

  ```azcli
  kubectl describe job rotate-creds --namespace ag1
  ```

  作业成功后，将更新一个 SQL Server 实例的主密钥和 `sa` 密码。


1. 再次运行作业之前，请删除作业。 作业名称必须唯一。

  ```azurecli
  kubectl delete job rotate-creds --namespace ag1
  ```

若要为所有 SQL Server 实例设置相同的 `sa` 密码，请对每个 SQL Server 实例重复以上步骤。

## <a name="next-steps"></a>后续步骤

[使用 Azure Kubernetes 服务 (AKS) 访问 Kubernetes 仪表板](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Kubernetes 群集上的 SQL Server 可用性组](sql-server-ag-kubernetes.md)
