---
title: 与大数据群集在 Kubernetes 的 SQL Server 的数据持久性 |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 942442bca18e836c4f8711abc808a89649ff8593
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2018
ms.locfileid: "49460572"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>与 SQL Server 大数据群集在 Kubernetes 上的数据持久性

[永久性卷](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)提供插件模型，在其中存储如何提供的 Kubernetes 中的存储是抽象的使用方式已完成。 因此，可以将高可用存储，并将其插入 SQL Server 大数据群集群集。 这样，您完全控制的存储、 可用性和性能所需的类型。 Kubernetes 支持各种类型的存储解决方案，包括 Azure 磁盘/文件、 NFS、 本地存储和的详细信息。

## <a name="configure-persistent-volumes"></a>配置永久性卷

SQL Server 大数据群集使用这些持久卷的方法是通过使用[存储类](https://kubernetes.io/docs/concepts/storage/storage-classes/)。 可以创建不同的存储类的不同种类的存储，并在大数据群集部署时指定它们。 你可以配置要用于哪些用途 （池） 的存储类。 SQL Server 大数据群集创建[永久性卷声明](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)替换为需要永久卷每个 pod 的指定的存储类名称。 它然后装载在 pod 中相应的永久性卷。

> [!NOTE]

> CTP 2.0 中，仅为`ReadWriteOnce`支持整个群集的访问模式。

## <a name="deployment-settings"></a>部署设置

若要在部署期间使用持久性存储区，配置**USE_PERSISTENT_VOLUME**并**STORAGE_CLASS_NAME**环境变量，然后再运行`mssqlctl create cluster`命令。 **USE_PERSISTENT_VOLUME**设置为`true`默认情况下。 可以重写默认值并将其设置为`false`和 SQL Server 大数据群集在这种情况下，使用 emptyDir 装载。 

> [!WARNING]
> 没有永久性存储的情况下运行可能会导致无法正常工作的群集。 在 pod 重新启动时，群集元数据和/或用户数据将永久丢失。

如果将标志设置为 true 时，还必须提供**STORAGE_CLASS_NAME**作为在部署时参数。

## <a name="aks-storage-classes"></a>AKS 存储类

附带了 AKS[两个内置的存储类](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv)**默认**并**托管高级**以及为其预配的动态程序。 可以指定任何一项都或创建您自己的存储类用于大数据群集部署与已启用的持久存储。

## <a name="minikube-storage-class"></a>Minikube 存储类

Minikube 附带了一个名为的内置存储类**标准**以及为其动态预配程序。 请注意，在 Minikube，如果 USE_PERSISTENT_VOLUME = true （默认值），因为默认值不同，还必须替代 STORAGE_CLASS_NAME 环境变量的默认值。 将值设置为`standard`: 
```
SET STORAGE_CLASS_NAME=standard
```

或者，可以禁止在 Minikube 上使用永久性卷：
```
SET USE_PERSISTENT_VOLUME=false
```


## <a name="kubeadm"></a>Kubeadm

Kubeadm 不随一个内置的存储类;因此，我们已创建脚本以设置永久性卷和存储类使用本地存储或[车](https://github.com/rook/rook)存储。

## <a name="on-premises-cluster"></a>在本地群集

在本地群集显然不带任何内置的存储类，因此你必须设置[永久性卷](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)/[配置程序](https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/)事先，然后使用相应在 SQL Server 大数据群集部署过程中的存储类。

# <a name="customize-storage-size-for-each-pool"></a>自定义每个池的存储大小
默认情况下，预配为每个群集中预配 pod 永久性卷的大小为 6 GB。 这通过设置环境变量是可配置`STORAGE_SIZE`为不同的值。 例如，运行以下命令来运行之前将值设置为 10 GB 为`mssqlctl create cluster command`。

```bash
export STORAGE_SIZE=10Gi
```

此类存储类名称和群集中不同的池的永久性卷大小，还可以具有不同配置的永久性存储设置。 例如，可以配置永久性卷用于存储池使用不同的存储类，并具有更高的容量部署的部署群集之前设置以下环境变量：

```bash
export STORAGE_POOL_USE_PERSISTENT_VOLUME=true
export STORAGE_POOL_STORAGE_CLASS_NAME=managed-premium
export STORAGE_POOL_STORAGE_SIZE=100Gi
```

下面是相关设置 SQL Server 大数据群集的持久性存储的环境变量的完整列表：

| 环境变量 | 默认值 | Description |
|---|---|---|
| **USE_PERSISTENT_VOLUME** | true | `true` 若要使用 Kubernetes 永久性卷声明 pod 存储。 `false` 使用临时主机存储为 pod 存储。 |
| **STORAGE_CLASS_NAME** | 默认值 | 如果`USE_PERSISTENT_VOLUME`是`true`这指示要使用的 Kubernetes 存储类的名称。 |
| **STORAGE_SIZE** | 6 gi | 如果`USE_PERSISTENT_VOLUME`是`true`，这表示每个 pod 的永久性卷大小。 |
| **DATA_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` 若要使用 Kubernetes 永久性卷声明为 pod 中的数据池。 `false` 要用于数据池 pod 的临时主机存储。 |
| **DATA_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | 指示要用于关联数据池 pod 使用永久性卷的 Kubernetes 存储类的名称。|
| **DATA_POOL_STORAGE_SIZE** | STORAGE_SIZE |指示数据池中每个 pod 的永久性卷大小。 |
| **STORAGE_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` 若要使用 Kubernetes 永久性卷声明为存储池中的 pod。 `false` 要用于存储池 pod 的临时主机存储。|
| **STORAGE_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | TIndicates Kubernetes 存储类用于与存储池 pod 相关联的持久卷的名称。 |
| **STORAGE_POOL_STORAGE_SIZE** | STORAGE_SIZE | 指示在存储池中每个 pod 的永久性卷大小。 |

## <a name="next-steps"></a>后续步骤

有关在 Kubernetes 中的卷的完整文档，请参阅[卷上的 Kubernetes 文档](https://kubernetes.io/docs/concepts/storage/volumes/)。

有关部署 SQL Server 大数据群集的详细信息，请参阅[如何部署大数据群集在 Kubernetes 的 SQL Server](deployment-guidance.md)。

