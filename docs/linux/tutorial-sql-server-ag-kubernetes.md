---
title: 在 Kubernetes 中的 Docker 容器上配置 SQL Server Always On 可用性组 |Microsoft Docs
description: 本教程演示如何部署 SQL Server always on 可用性组与 Azure 容器服务上的 Kubernetes。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: tutorial
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux,mvc
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6d21866f3f7004dff1ea86ca4f608580a79ab754
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049357"
---
# <a name="configure-a-sql-server-always-on-availability-group-on-docker-containers-in-kubernetes-with-azure-kubernetes-service-aks"></a>在 Kubernetes Azure Kubernetes 服务 (AKS) 中的 Docker 容器上配置 SQL Server Always On 可用性组

本教程演示如何在 AKS 上的容器中配置高度可用的 SQL Server 实例。 此外可以[部署 Kubernetes 中的 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)。 若要比较两个不同的 Kubernetes 解决方案，请参阅[SQL Server 容器的高可用性](sql-server-linux-container-ha-overview.md)。

在本教程中，您学习如何：  

> [!div class="checklist"]
> * 创建存储
> * 将 SQL Server 运算符部署到 Kubernetes 群集 
> * 创建 Kubernetes 机密
> * 部署 SQL Server 实例和运行状况代理
> * 连接到主副本
> * 将数据库添加到可用性组

本教程演示了中的体系结构[Azure Kubernetes 服务 (AKS)](http://docs.microsoft.com/azure/aks/)。 如果还没有 Azure 订阅，创建[免费帐户](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)在开始之前。

此关系图表示在本教程中所做的解决方案：

![kubernetes ag 群集](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

### <a name="deployment-methodology-for-kubernetes"></a>适用于 Kubernetes 的部署方法

这篇文章中的步骤的几个创建清单，并随后部署到群集的清单。 清单是 yaml 文件部署的 Kubernetes 对象的描述。

在此示例中的.yaml 文件位于[sql server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability)。

对象包括存储、 运算符、 pod、 容器和服务。

## <a name="prerequisites"></a>必要條件

* 常规熟悉这些技术

  * [Kubernetes](http://kubernetes.io) 1.8 版
  * [Azure Kubernetes 服务 (AKS)](http://docs.microsoft.com/azure/aks/)
  * [Docker 上的 SQL Server](quickstart-install-connect-docker.md)
  * [SQL Server Always On 可用性组](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

* 具有四个节点的 Kubernetes 群集。

  有关说明，请参阅[教程： 部署 Azure Kubernetes 服务 (AKS) 群集](http://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster)。

* 安装[ `kubectl` ](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster#install-the-kubectl-cli)。

## <a name="configuration-and-deployment-procedures"></a>配置和部署过程

本教程将演示如何将.yaml 文件应用于 Kubernetes 群集。

## <a name="create-the-secrets"></a>创建机密

若要创建 Kubernetes 机密来存储 SQL Server SA 帐户和 SQL Server 主密钥的密码，请运行以下命令。

```azurecli
kubectl create secret generic sql-secrets --from-literal=sapassword="MyC0m9l&xP@ssw0rd" --from-literal=masterkeypassword="MyC0m9l&xP@ssw0rd2"
```

在生产环境中使用不同的复杂密码。

## <a name="deploy-the-operator"></a>部署运算符

Kubernetes 运算符部署的 SQL Server 实例和在 Kubernetes 群集中配置可用性组。 

请参阅上的示例操作员 [`operator.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml)

下载`operator.yaml`从[sql server 示例](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/)

将运算符部署为一个副本 Kubernetes 部署。

若要部署该运算符：

部署与运算符`kubectl apply`命令。

```azurecli
kubectl apply -f operator.yaml
```

## <a name="create-the-sql-server-ag-deployment"></a>创建 SQL Server 可用性组部署

下一步创建一个 Kubernetes 部署中的 SQL Server 实例和可用性组。 此部署应用到群集后，该运算符将作为 Docker 容器部署的 SQL Server 实例。 此部署将导致使用一个 pod 的三个 StatefulSets。 每个 pod 将包括两个容器：

* SQL Server 实例基于`mssql-server`图像
* HA 监督程序

此外，部署说明了可用性组侦听器的负载均衡器服务

若要部署服务器的 mssql:

1. 复制[sqlserver.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml)到您的计算机。
2. 更新`sqlserver.yaml`为您的环境。


若要部署的 SQL Server 实例并创建可用性组，请运行以下命令。

```azurecli
kubectl apply -f sqlserver.yaml
```

## <a name="deploy-ag-services"></a>部署 AG 服务

在 Kubernetes 群集中创建负载均衡器服务添加到可用性组中的副本直接调用。

[ag services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)创建四个服务。

* ag1 主连接到主副本。
* ag1 辅助数据库同步连接到同步次要副本。
* ag1 辅助异步连接到异步辅助副本。
* ag1 辅助数据库配置连接到仅配置副本。 

  >[!NOTE]
  >这些负载均衡器服务提供作为示例。 在本教程中没有仅配置副本。


部署负载均衡器服务，因此可以连接到可用性组。

若要部署服务，运行以下命令。

```azurecli
kubectl apply -f ag-services.yaml
```

### <a name="monitor-the-deployment"></a>监视部署

可以使用[Kubernetes 仪表板与 Azure Kubernetes 服务 (AKS)](https://docs.microsoft.com/en-us/azure/aks/kubernetes-dashboard)来监视部署。 

使用`az aks browse`以启动仪表板。 

在部署后，可以更新仅可用性组的成员身份列表和初始化后的 T-SQL 脚本。 无法更新其他属性-必须删除并重新创建该资源。 可以使用旋转的自动生成的用户凭据`mssql-server-k8s-rotate-creds`作业。

## <a name="connect-to-the-sql-server-instance-hosting-the-primary-replica"></a>连接到承载主副本的 SQL Server 实例

`ag-services.yaml`介绍了 Kubernetes 服务名称`ag1-primary`。 `ag1-primary` 创建指向托管主副本的 SQL Server 实例的 Azure 负载均衡器。 为目标服务器，使用该服务的外部 IP 地址`sa`方式帐户和密码你前面创建`mssql secret`的密码。

使用`kubectl get services`获取此 IP 地址。

例如：

![获取服务示例](media\tutorial-sql-server-ag-containers-kubernetes\KubernetesGetServices.png)

在上面，图像中`ag1-primary`服务具有外部的 IP 地址的`104.42-50.138`。 

若要使用 SQL 身份验证连接到 SQL Server，请使用`sa`帐户、 的值为`sapassword`从所创建的机密和此 IP 地址。

例如：

```cmd
sqlcmd -S 104.42.50.138 -U sa -P "MyC0m9l&xP@ssw0rd"
```

![使用 sqlcmd 连接](./media/tutorial-sql-server-ag-containers-kubernetes/sqlcmdConnect.png)

你还可以使用连接[SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。

若要验证你的连接，请到承载主副本的 SQL Server 实例运行以下查询：

```sql
SELECT @@SERVERNAME;
```

查询将返回承载主副本的 SQL Server 实例的名称。

此时，Kubernetes 群集具有三个 docker 容器中的 SQL Server 实例。 可用性组跨所有三个 SQL Server 实例，但没有数据库位于可用性组中。 下一步是将数据库添加到可用性组。

## <a name="add-a-database-to-the-availability-group"></a>将数据库添加到可用性组

若要将数据库添加到可用性组：

1. 创建数据库

  ```sql
  CREATE DATABASE [DemoDB]
  ```

1. 执行完整备份的数据库启动的事务日志链

  ```sql
  BACKUP DATABASE [DemoDB] 
  TO  DISK = N'/var/opt/mssql/data/DemoDB.bak' 
    WITH NOFORMAT, 
    NOINIT,  
    NAME = N'DemoDB-Full Database Backup', 
    SKIP, 
    NOREWIND, 
    NOUNLOAD,  
    STATS = 10;
  GO
  ```

1. 将数据库添加到可用性组

  ```sql
  ALTER AVAILABILITY GROUP ag1 ADD DATABASE [DemoDB]; 
  ```

在副本自动配置自动种子设定模式使可用性组设定到次要副本上的数据库的种子。

在 SQL Server Management Studio，可以连接到主副本，并查看仪表板中的可用性组。

下面的示例显示在仪表板中配置的三个节点上的可用性组的副本。

![AG1 仪表板](./media/tutorial-sql-server-ag-containers-kubernetes/ssms_AG1.png)

## <a name="verify-failure-and-recovery"></a>验证故障与恢复

若要验证故障检测和故障转移可以删除承载主副本的 pod。 Kubernetes 将选择新的主副本和重定向侦听器。 然后它将重新创建已删除的 pod。 

若要演示此过程，请执行以下步骤：

1. 列出运行 SQL Server 的 pod。

   ```azurecli
   kubectl get pods
   ```

2. 确定 pod 正在运行的主副本。

   可以连接到主副本使用的外部 IP 和查询`@@servername`或使用`kubectl`以获取相应的 pod。 此命令将返回包含容器运行可用性组的主副本 pod 的名称：

   ```azurecli
   kubectl get pods --selector="role.ag.mssql.microsoft.com/ag1"="primary" --output=jsonpath={.items..metadata.name}
   ```

3. 删除 pod。

   ```azurecli
   kubectl delete pod <podName>
   ```

替换为`<podName>`pod 名称将前一步骤返回的值。 

Kubernetes 自动故障转移到其中一个可用的同步辅助副本，以及重新创建已删除的 pod。

## <a name="clean-up-resources"></a>清理资源

不再需要时，删除资源组和所有相关的资源。 运行以下命令：
>[!WARNING]
>此命令完全删除资源组中的所有内容。 删除资源组后，没有任何 Kubernetes 群集的组件将可用。

```azurecli
az group delete --name <MyResourceGroup>
```

若要运行上面的命令，替换`<MyResourceGroup>`与资源组的名称。 

Azure 将删除资源组。

## <a name="summary"></a>总结

在本教程中，您学习了如何：  

> [!div class="checklist"]
> * 创建存储
> * 将 SQL Server 运算符部署到 Kubernetes 群集 
> * 创建 Kubernetes 机密
> * 部署 SQL Server 实例和运行状况代理
> * 连接到主副本
> * 将数据库添加到可用性组

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
>[Kubernetes 简介](http://docs.microsoft.com/azure/aks/intro-kubernetes)
>[管理 Kubernetes 上的 SQL Server](sql-server-linux-kubernetes-manage.md)