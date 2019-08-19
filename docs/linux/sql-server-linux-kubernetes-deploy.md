---
title: 在 Kubernetes 群集上部署 SQL Server Always On 可用性组
description: 本文介绍 SQL Server Kubernetes Always On 可用性组运算符全局要求的参数
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 10/02/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1e8825336edd4e55812f6037bbb4479a3b225e3f
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028728"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-a-kubernetes-cluster"></a>在 Kubernetes 群集上部署 SQL Server Always On 可用性组

本文中的示例在具有三个副本的 Kubernetes 群集上部署了 SQL Server Always On 可用性组。 次要副本处于同步提交模式。

在 Kubernetes 上，该部署包括 SQL Server 运算符、SQL Server 容器和负载均衡器服务。 运算符自动协调可用性组。 本文介绍如何执行以下操作：

- 部署运算符、SQL Server 容器和负载均衡服务。
- 使用服务连接到可用性组。
- 将数据库添加到可用性组。

## <a name="requirements"></a>要求

- 具有最新版本的 AKS Kubernetes 群集
- 至少三个节点
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- 访问 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) GitHub 存储库

> [!NOTE]
> 可使用任何类型的 Kubernetes 群集。 若要在 Azure Kubernetes 服务 (AKS) 上创建 Kubernetes 群集，请参阅[创建 AKS 群集](https://docs.microsoft.com/azure/aks/create-cluster)。
>
> 使用最新版本的 Kubernetes。 具体版本取决于用户的订阅和区域。 请参阅 [AKS 中支持的 Kubernetes 版本](https://docs.microsoft.com/azure/aks/supported-kubernetes-versions)。  
>
> 以下脚本在 Azure 中创建了一个四节点 Kubernetes 群集。 运行脚本之前，请将 `<latest version>` 替换为最新的可用版本。 例如 `1.12.5`。
>
> ```azure-cli
> az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version <latest version> --generate-ssh-keys
> ```

## <a name="deploy-the-operator-sql-server-containers-and-load-balancing-services"></a>部署运算符、SQL Server 容器和负载均衡服务

1. 创建[命名空间](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)。

      此示例使用名为 `ag1` 的命名空间。 运行以下命令以创建命名空间。
    
      ```azurecli
      kubectl create namespace ag1
      ```
    
      属于此解决方案的所有对象都位于 `ag1` 命名空间中。

1. 配置和部署 SQL Server 运算符清单。

      从 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) 复制 SQL Server [`operator.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml) 文件。
    
      `operator.yaml` 文件是 Kubernetes 运算符的部署清单。
    
      将清单应用到 Kubernetes 群集。
    
      ```azurecli
      kubectl apply -f operator.yaml --namespace ag1
      ```
    
1. 使用 `sa` 帐户密码和 SQL Server 实例主密钥为 Kubernetes 创建一个机密。

      使用 `kubectl` 创建机密。
      
      以下示例将在 `ag1` 命名空间中创建一个名为 `sql-secrets` 的机密。 机密存储两个密码：
      
      - `sapassword` 存储 SQL Server `sa` 帐户的密码。
      - `masterkeypassword` 存储用于创建 SQL Server 主密钥的密码。 
    
   将脚本复制到终端。 将每个 `<>` 替换为复杂密码并运行该脚本以创建机密。
    
   >[!NOTE]
   >密码不能使用 `&` 或 `` ` `` 字符。
    
   ```azurecli
   kubectl create secret generic sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
   ```

1. 部署 SQL Server 自定义资源。

      从 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) 复制 SQL Server 清单 [`sqlserver.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml)。
    
      >[!NOTE]
      >`sqlserver.yaml` 文件描述了每个 SQL Server 实例所需的 SQL Server 容器、持久卷声明、持久卷和负载均衡服务。
    
      将清单应用到 Kubernetes 群集。
    
      ```azurecli
      kubectl apply -f sqlserver.yaml --namespace ag1
      ```
      
下图显示了此示例中 `kubectl apply` 的成功应用。

![创建 sqlservers](./media/sql-server-linux-kubernetes-deploy/create-sqlservers.png)

应用 SQL Server 清单后，运算符将部署 SQL Server 容器。

Kubernetes 将容器置于 Pod 中。 使用 `kubectl get pods --namespace ag1` 查看 Pod 状态。 下图显示了部署 SQL Server Pod 后的示例部署。 

![生成 Pod](./media/sql-server-linux-kubernetes-deploy/builtpods.png)

### <a name="monitor-the-deployment"></a>监视部署

可以使用[具有 Azure Kubernetes 服务的 Kubernetes 仪表板](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)来监视部署。

使用 `az aks browse` 启动仪表板。 

## <a name="connect-to-the-availability-group-with-the-services"></a>使用服务连接到可用性组

[sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) 示例中的 [`ag-services.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) 描述了可连接到可用性组副本的负载均衡服务。 

- `ag1-primary` 提供连接到主要副本的终结点。
- `ag1-secondary` 提供连接到任何次要副本的终结点。

应用清单文件时，Kubernetes 将为每种类型的副本创建负载均衡服务。 负载均衡服务包括 IP 地址。 使用此 IP 地址可连接到所需的副本类型。

若要部署服务，请运行以下命令。

```azurecli
kubectl apply -f ag-services.yaml --namespace ag1
```

部署服务后，使用 `kubectl get services --namespace ag1` 标识服务的 IP 地址。

利用 IP 地址，可以连接到托管每种类型副本的 SQL Server 实例。

下图显示的内容：

- 命名空间 `ag1` 的 `kubectl get services` 输出。

- 为每个 SQL Server 容器创建的负载均衡服务。 使用这些 IP 地址作为终结点，直接连接到群集中的 SQL Server 实例。

- 使用 `sa` 帐户通过负载均衡器终结点将 `sqlcmd` 连接到主要副本。

![连接](./media/sql-server-linux-kubernetes-deploy/connect.png)

## <a name="add-a-database-to-the-availability-group"></a>将数据库添加到可用性组

>[!NOTE]
>当前 SQL Server Management studio 不能将数据库添加到可用性组。 使用 Transact-SQL。

Kubernetes 创建 SQL Server 容器后，请完成以下步骤以将数据库添加到可用性组。

1. [连接](sql-server-linux-kubernetes-connect.md)到群集中的 SQL Server 实例。

1. 创建数据库。

      ```sql
      CREATE DATABASE [demodb]
      ```

1. 对数据库执行完整备份以启动日志链。

      ```sql
      USE MASTER
      GO
      BACKUP DATABASE [demodb] 
      TO DISK = N'/var/opt/mssql/data/demodb.bak'
      ```

1. 将数据库添加到可用性组。

      ```sql
      ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [demodb]
      ```
    
可用性组通过自动种子设定进行创建，以便 SQL Server 自动创建紫瑶副本。

可以从 SQL Server Management Studio 可用性组仪表板中查看可用性组的状态。

![面板](./media/sql-server-linux-kubernetes-deploy/dashboard.png)

## <a name="next-steps"></a>后续步骤

- [连接到 Kubernetes 群集上的 SQL Server 可用性组](sql-server-linux-kubernetes-connect.md)

- [管理 Kubernetes 群集上的 SQL Server 可用性组](sql-server-linux-kubernetes-manage.md)

- [SQL Server 支持 Kubernetes 群集中容器上的可用性组](sql-server-ag-kubernetes.md)
