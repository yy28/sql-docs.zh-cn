---
title: 部署 SQL Server Always On Kubernetes 群集上的可用性组
description: 本文介绍的 SQL Server Kubernetes Always On 可用性组运算符全局要求的参数
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fe736fa57ea85e92b69d12f44fca35f4097cd3d6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48160057"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-kubernetes-cluster"></a>部署 SQL Server Alwayson 可用性组在 Kubernetes 群集

## <a name="requirements"></a>要求

- Kubernetes 群集
- Kubernetes 1.11.0 版本或更高版本
- 四个或多个节点
- [kubectl](http://kubernetes.io/docs/tasks/tools/install-kubectl/)。

  >[!NOTE]
  >可以使用任何类型的 Kubernetes 群集。 若要在 Azure Kubernetes 服务 (AKS) 创建 Kubernetes 群集，请参阅[创建 AKS 群集](http://docs.microsoft.com/azure/aks/create-cluster)。
  > 以下脚本在 Azure 中创建一个四个节点的 Kubernetes 群集。
  >```azure-cli
  az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version 1.11.1
  >```

## <a name="steps"></a>步骤

1. 配置存储

  在 Azure 等云环境，配置[永久性卷](http://kubernetes.io/docs/concepts/storage/persistent-volumes/)为每个 SQL Server 实例。

  若要在 Azure 中创建永久性卷，请参阅`pv.yaml`并`pvc.yaml`中[sql server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/templates)。

  若要创建的存储空间，运行以下命令：

  ```azurecli
  kubectl apply -f <pv.yaml>
  ```

1. 创建 Kubernetes 机密的 SA 密码和主密钥。

  以下示例创建两个密码。 `sapassword` 是的 SA 密码和`masterkeypassword`是为主密钥。 在运行此脚本替换为之前`<MyC0mp13xP@55w04d!>`替换为每个机密的不同复杂密码。

   ```azurecli
   kubectl create secret generic sql-secrets --from-literal='sapassword=<MyC0mp13xP@55w04d!>' --from-literal='masterkeypassword=<MyC0mp13xP@55w04d!>'
   ```

1. 配置和部署 SQL Server 运算符清单。

  复制 SQL Server 运算符`operator.yaml`文件从[sql server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)。

  `operator.yaml`文件是 Kubernetes 运算符部署 manifiest。

  若要配置清单，请更新`operator.yaml`文件为您的环境。

  适用于 Kubernetes 群集清单。

  ```azurecli
  kubectl apply -f operator.yaml
  ```

1. 部署 SQL Server 自定义资源。

  复制 SQL Server 清单`sqlserver.yaml`从[sql server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)。

  适用于 Kubernetes 群集清单。

  ```azurecli
  kubectl apply -f sqlserver.yaml
  ```

部署 SQL Server 清单后，该运算符将 SQL Server 的实例部署为容器中的 pod。

在脚本完成后，存储、 SQL Server 实例、 负载均衡器服务将创建 Kubernetes 运算符。 你可以监视与部署[Kubernetes 仪表板](http://docs.microsoft.com/azure/aks/kubernetes-dashboard)。

Kubernetes 创建后的 SQL Server 容器将完成以下步骤以将数据库添加到可用性组：

1. [连接](sql-server-linux-kubernetes-connect.md)到群集中的 SQL Server 实例。

1. 创建数据库。

1. 执行完整备份的数据库，以启动日志链。

1. 将数据库添加到可用性组。

使用自动种子设定使 SQL Server 将自动创建辅助副本创建可用性组。

## <a name="next-steps"></a>后续步骤

[连接到 Kubernetes 群集上的 SQL Server 可用性组](sql-server-linux-kubernetes-connect.md)

[管理 Kubernetes 群集上的 SQL Server 可用性组](sql-server-linux-kubernetes-manage.md)

[Kubernetes 群集上的 SQL Server 可用性组](sql-server-ag-kubernetes.md)
