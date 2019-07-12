---
title: 部署 SQL Server Always On 可用性组上的 Kubernetes 群集
description: 本文介绍的 SQL Server Kubernetes Always On 可用性组运算符全局要求的参数
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 10/02/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 88b3b2a8c955c628284bec59c9e9fead98e174b8
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833243"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-a-kubernetes-cluster"></a>部署 SQL Server Always On 可用性组上的 Kubernetes 群集

此文章中的示例部署 Kubernetes 群集具有三个副本上的 SQL Server Always On 可用性组。 辅助副本处于同步提交模式。

在 Kubernetes 上部署包括 SQL Server 运算符、 SQL Server 容器和负载均衡器服务。 运算符可自动协调可用性组。 此文章介绍了如何：

- 运算符、 SQL Server 容器和负载均衡的服务部署。
- 连接到与服务的可用性组。
- 将数据库添加到可用性组。

## <a name="requirements"></a>要求

- 包含最新版本的 AKS 的 Kubernetes 群集
- 至少三个节点
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- 访问权限[sql server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)GitHub 存储库

> [!NOTE]
> 可以使用任何类型的 Kubernetes 群集。 若要在 Azure Kubernetes 服务 (AKS) 创建 Kubernetes 群集，请参阅[创建 AKS 群集](https://docs.microsoft.com/azure/aks/create-cluster)。
>
> 使用 Kubernetes 的最新版本。 特定版本取决于你的订阅和区域。 请参阅[在 AKS 中的支持 Kubernetes 版本](https://docs.microsoft.com/en-us/azure/aks/supported-kubernetes-versions)。  
>
> 以下脚本在 Azure 中创建四个节点 Kubernetes 群集。 在运行脚本替换为之前`<latest version>`使用最新的版本。 例如 `1.12.5`。
>
> ```azure-cli
> az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version <latest version> --generate-ssh-keys
> ```

## <a name="deploy-the-operator-sql-server-containers-and-load-balancing-services"></a>部署运算符、 SQL Server 容器和负载均衡的服务

1. 创建[命名空间](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)。

      此示例使用名为命名空间`ag1`。 运行以下命令以创建命名空间。
    
      ```azurecli
      kubectl create namespace ag1
      ```
    
      属于此解决方案的所有对象都都在`ag1`命名空间。

1. 配置和部署 SQL Server 运算符清单。

      将 SQL Server 复制[ `operator.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml)文件[sql server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)。
    
      `operator.yaml`文件是 Kubernetes 运算符的部署清单。
    
      适用于 Kubernetes 群集清单。
    
      ```azurecli
      kubectl apply -f operator.yaml --namespace ag1
      ```
    
1. 对于 Kubernetes 使用密码创建机密`sa`帐户和 SQL Server 实例的主密钥。

      创建与机密`kubectl`。
      
      下面的示例创建名为的机密`sql-secrets`在`ag1`命名空间。 机密存储两个密码：
      
      - `sapassword` 将密码存储为 SQL Server`sa`帐户。
      - `masterkeypassword` 存储用于创建 SQL Server 主密钥的密码。 
    
   将脚本复制到你的终端。 将为每个`<>`使用复杂密码和运行该脚本创建机密。
    
   >[!NOTE]
   >不能使用密码`&`或`` ` ``字符。
    
   ```azurecli
   kubectl create secret generic sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
   ```

1. 部署 SQL Server 自定义资源。

      复制 SQL Server 清单[ `sqlserver.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml)从[sql server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)。
    
      >[!NOTE]
      >`sqlserver.yaml`文件介绍了 SQL Server 容器、 永久性卷声明、 永久性卷和负载均衡的服务所需的每个 SQL Server 实例。
    
      适用于 Kubernetes 群集清单。
    
      ```azurecli
      kubectl apply -f sqlserver.yaml --namespace ag1
      ```
      
下图显示了成功的应用程序的`kubectl apply`对于此示例。

![创建 sqlservers](./media/sql-server-linux-kubernetes-deploy/create-sqlservers.png)

应用 SQL Server 清单后，该运算符将部署 SQL Server 容器。

Kubernetes 置于 pod 中容器。 使用`kubectl get pods --namespace ag1`来查看 pod 的状态。 下图显示示例部署中部署 SQL Server pod 之后。 

![生成 pod](./media/sql-server-linux-kubernetes-deploy/builtpods.png)

### <a name="monitor-the-deployment"></a>监视部署

可以使用[使用 Azure Kubernetes 服务的 Kubernetes 仪表板](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)来监视部署。

使用`az aks browse`以启动仪表板。 

## <a name="connect-to-the-availability-group-with-the-services"></a>连接到与服务的可用性组

[ `ag-services.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml)从[sql server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)示例介绍了可以连接到可用性组副本的负载平衡服务。 

- `ag1-primary` 提供了终结点以连接到主副本。
- `ag1-secondary` 提供了终结点以连接到任何辅助副本。

在应用清单文件时，Kubernetes 创建副本的每种类型的负载平衡服务。 负载平衡服务包括一个 IP 地址。 使用此 IP 地址连接到副本所需的类型。

若要部署服务，运行以下命令。

```azurecli
kubectl apply -f ag-services.yaml --namespace ag1
```

部署服务后，使用`kubectl get services --namespace ag1`来标识服务的 IP 地址。

使用 IP 地址，你可以连接到 SQL Server 实例承载副本的每种类型。

下图显示了：

- 从输出`kubectl get services`命名空间`ag1`。

- 为每个 SQL Server 容器创建负载均衡服务。 使用这些 IP 地址作为终结点直接连接到群集中的 SQL Server 实例。

- `sqlcmd`连接到主副本与`sa`通过负载均衡器终结点的帐户。

![连接](./media/sql-server-linux-kubernetes-deploy/connect.png)

## <a name="add-a-database-to-the-availability-group"></a>将数据库添加到可用性组

>[!NOTE]
>在此期间，SQL Server Management Studio 无法将数据库添加到可用性组。 使用 Transact SQL。

Kubernetes 创建 SQL Server 容器后，完成以下步骤以将数据库添加到可用性组。

1. [连接](sql-server-linux-kubernetes-connect.md)到群集中的 SQL Server 实例。

1. 创建数据库。

      ```sql
      CREATE DATABASE [demodb]
      ```

1. 执行完整备份的数据库，以启动日志链。

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
    
使用自动种子设定，以便 SQL Server 将自动创建辅助副本创建可用性组。

可以查看 SQL Server Management Studio 可用性组仪表板中的可用性组的状态。

![面板](./media/sql-server-linux-kubernetes-deploy/dashboard.png)

## <a name="next-steps"></a>后续步骤

- [连接到 Kubernetes 群集上的 SQL Server 可用性组](sql-server-linux-kubernetes-connect.md)

- [管理 Kubernetes 群集上的 SQL Server 可用性组](sql-server-linux-kubernetes-manage.md)

- [SQL Server 上的 Kubernetes 群集中的容器支持可用性组](sql-server-ag-kubernetes.md)
