---
title: 管理 SQL Server Always On 可用性组 Kubernetes
description: 本文介绍如何管理 SQL Server Always On 可用性组在 Kubernetes 中。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 808f49ff5060ba6a6ffe9e864cfc2710fe6251e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705524"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>管理 SQL Server Alwayson 可用性组 Kubernetes

若要管理 Always On 可用性组在 Kubernetes 上，创建一个清单，并将其应用到群集。 该清单是`.yaml`文件。  

这篇文章中的示例适用于所有 Kubernetes 群集。 在这些示例方案将应用针对在 Azure Kubernetes 服务群集。

在完整的部署示例，请参阅[部署 SQL Server Always On 可用性组 Kubernetes 群集上](sql-server-linux-kubernetes-deploy.md)。

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>故障转移-在 Kubernetes 上的 SQL Server 可用性组

若要故障转移或将主副本移至可用性组中的其他节点，请完成以下步骤：

1. 在清单文件中定义一个作业。

  [`failover.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/failover.yaml) -在[sql server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)github 存储库介绍故障转移作业。

  将清单文件复制到您管理终端。

  更新你的环境的文件。

  - 替换为`<containerName>`与预期的可用性组目标的 pod 名称 (例如 mssql2-0)。
  - 如果可用性组不在`ag1`命名空间中，将为`ag1`与命名空间。

  此文件定义一个名为故障转移作业`manual-failover`。

1. 若要部署作业，请使用`kubectl apply`。 以下脚本将部署作业。

  ```azurecli
  kubectl apply -f failover.yaml
  ```

  部署作业后，kubernetes，使用 SQL Server 运算符，执行以下任务：
  
  - 将降级为次要副本的主副本
  
  - 将升级为主要副本的指定的副本
  
  应用清单文件后，Kubernetes 运行作业。 该作业可以选择新的主管监督程序，并将主副本移动到 SQL Server 实例的领导。

1. 验证作业已完成。
  
  Kubernetes 运行该作业后，可以查看日志。
  
  下面的示例返回名为的作业状态`manual-failover`。

  ```azurecli
  kubectl describe jobs/manual-failover --namespace ag1
  ```

1. 删除手动故障转移作业。 

  >[!IMPORTANT]
  >颁发另一个的手动故障转移之前，你必须手动删除该作业。
  > 
  >在 Kubernetes 中的作业对象会保留在完成后，以便可以查看其状态。 需要注意的它们的状态后手动删除旧作业。 删除作业也会删除 Kubernetes 日志。 如果你不删除该作业，未来的故障转移作业将失败，除非您更改的作业名称和 pod 选择器。 有关详细信息，请参阅[完成运行作业-](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)。

  以下命令将删除该作业。

  ```azurecli
  kubectl delete jobs manual-failover --namespace ag1
  ```

## <a name="rotate-credentials"></a>滚动更新凭据

轮换凭据重置密码的 SQL Server`sa`帐户和 SQL Server[服务主密钥](../relational-databases/security/encryption/service-master-key.md)。 

若要完成此任务，将在 Kubernetes 群集中创建新的机密，然后创建一个作业来轮换凭据。

轮换凭据时之前, 进行新的机密的密码和主密钥。

以下脚本将创建名为机密`new-sql-secrets`。 在运行该脚本之前，替换`<>`复杂的密码与`sapassword`和`masterkeypassword`。 为每个相应的值使用不同的密码。

```azurecli
kubectl create secret generic new-sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
```

每个实例的 SQL Server 主密钥所需完成以下步骤或`sa`密码。

1. 复制[ `rotate-creds.yaml` ](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml)管理终端到。

  [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) 在中[sql server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/)github 存储库是为此作业的清单的示例。

  应用此清单之前，更新你的环境的清单。 查看和更改以下设置，根据需要。

  - 验证命名空间。 根据需要进行更新。 在清单中下面的示例适用于命名空间名为`ag1`。

    ```yaml
    metadata:
      name: rotate-creds
      namespace: ag1
    ```

  - 验证 SQL Server 实例的名称。 根据需要进行更新。 下面的示例清单规范中适用于 SQL Server 实例名为`mssql1`。

    ```yaml
    env:
      - name: MSSQL_K8S_SQL_SERVER_NAME
        value: mssql1
    ```

  将更新的清单文件保存到你的工作站。

1. 使用`kubectl`部署作业。

  ```azurecli
  kubectl apply -f rotate-creds.yaml --namespace ag1
  ```

  Kubernetes 更新主密钥和`sa`密码的 SQL Server 可用性组中的一个实例。

1. 验证作业已完成。 运行下面的命令：若要验证作业已完成，运行 

  ```azcli
  kubectl describe job rotate-creds --namespace ag1
  ```

  作业成功时，主密钥后和`sa`更新一个 SQL Server 实例的密码。


1. 重新运行该作业之前，请删除该作业。 每个作业名称必须是唯一的。

  ```azurecli
  kubectl delete job rotate-creds --namespace ag1
  ```

若要设置相同`sa`密码的所有实例的 SQL Server，SQL Server 的每个实例重复上述步骤。

## <a name="next-steps"></a>后续步骤

[访问 Kubernetes 仪表板与 Azure Kubernetes 服务 (AKS)](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Kubernetes 群集上的 SQL Server 可用性组](sql-server-ag-kubernetes.md)
