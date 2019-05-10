---
title: 在 Kubernetes 上的数据持久性
titleSuffix: SQL Server big data clusters
description: 了解如何在 SQL Server 2019 大数据群集中的数据暂留工作原理。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: d095af731e3c62ce24dd3d8cbf059aa6278dd22c
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64776158"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>与 SQL Server 大数据群集在 Kubernetes 上的数据持久性

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[永久性卷](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)为存储在 Kubernetes 中提供的插件模型。 如何提供存储被抽象的使用方式。 因此，可以将高度可用的存储，并将其插入到 SQL Server 大数据群集。 这样，您完全控制的存储、 可用性和性能所需的类型。 Kubernetes 支持各种类型的存储解决方案，包括 Azure 磁盘/文件、 NFS、 本地存储和的详细信息。

## <a name="configure-persistent-volumes"></a>配置永久性卷

SQL Server 大数据群集使用这些持久卷的方法是通过使用[存储类](https://kubernetes.io/docs/concepts/storage/storage-classes/)。 可以创建不同的存储类的不同种类的存储，并在大数据群集部署时指定它们。 可以配置的存储类和要在池级别用途使用的永久性卷声明大小。 SQL Server 大数据群集创建[永久性卷声明](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)替换为需要永久卷每个组件的指定的存储类名称。 它然后装载在 pod 中相应的永久性卷。 

## <a name="configure-big-data-cluster-storage-settings"></a>配置大数据群集存储设置

类似于其他自定义项，您可以指定存储设置的群集配置文件中在部署时，针对每个池和控制平面。 如果池规范中的没有存储配置设置，则将使用的控制平面存储设置。 这是可以包括在规范中的存储配置部分的一个示例：

```json
    "storage": 
    {
        "usePersistentVolume": true,
        "className": "managed-premium",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
    }
```

若要在部署期间使用持久性存储区，设置的值**usePersistentVolume**关键*true*并**className**想要使用的密钥的存储类的名称相应的池。 此外可以自定义部署的一部分创建的永久性卷声明的大小。 最佳做法是，我们建议使用具有存储类*保留*[回收策略](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)。

> [!NOTE]
> 在 ctp 版本 2.5 时，不能修改存储配置设置后期部署。 此外，仅`ReadWriteOnce`支持整个群集的访问模式。

> [!WARNING]
> 没有永久性存储的情况下运行可在测试环境中，但它可能会导致无法正常工作的群集。 在 pod 重新启动时，群集元数据和/或用户数据将永久丢失。 我们不建议在此配置中运行。 

[配置存储](#config-samples)部分提供有关如何配置 SQL Server 大数据群集部署的存储设置的更多示例。

## <a name="aks-storage-classes"></a>AKS 存储类

附带了 AKS[两个内置的存储类](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv)**默认**并**托管高级**以及为其预配的动态程序。 可以指定任何一项都或创建您自己的存储类用于大数据群集部署与已启用的持久存储。 默认情况下，生成适用于 aks 群集配置文件中*aks 开发 test.json*附带了所要使用的持久性存储区配置**托管高级**存储类。

> [!WARNING]
> 使用内置的存储类创建的永久性卷**默认**并**托管高级**具有的回收策略*删除*。 因此时您删除 SQL Server 大数据群集，永久性卷声明获取也被删除，而且然后持久卷。 你可以创建使用自定义存储类**azure 磁盘**与 privioner*保留*回收策略，如中所示[这](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes)一文。


## <a name="minikube-storage-class"></a>Minikube 存储类

Minikube 附带了一个名为的内置存储类**标准**以及为其动态预配程序。 内置的配置文件。 minikube *minikube 开发 test.json*控制平面规范中具有存储配置设置。相同的设置将应用于所有池规范。 此外可以自定义此文件的副本，并将其用于大数据群集部署在 minikube 上。 可以手动编辑自定义文件和更改你想要运行特定池以适应工作负荷的永久性卷声明的大小。 或者，请参阅[配置存储](#config-samples)有关如何执行操作的示例部分编辑使用*mssqlctl*命令。

## <a name="kubeadm-storage-classes"></a>Kubeadm 存储类

Kubeadm 没有附带内置的存储类。 必须创建自己的存储类和使用本地存储，或者你首选的预配程序，如永久性卷[车](https://github.com/rook/rook)。 在这种情况下，将设置**className**到你配置的存储类。 

> [!NOTE]
> 中的内置 kubeadm 的部署配置文件中*kubeadm 开发 test.json*的默认值为**usePersistentVolume**该键*true*，因此必须将该值设置有关**className**否则预部署验证将失败。 部署还具有一个验证步骤，检查存在的存储类，而不是必要的永久性卷。 您必须确保创建具体取决于你的群集的规模足够卷。 在 CTP2.5，对于默认群集大小必须创建至少 23 的卷。 [此处](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)示范了如何创建使用本地预配程序永久性卷。


## <a name="customize-storage-configurations-for-each-pool"></a>自定义的每个池的存储配置

对于所有自定义项，您必须首先创建一份内置你想要使用的配置文件中。 例如，以下命令将创建一份*aks 开发 test.json*当前目录中的部署配置文件：

```bash
mssqlctl cluster config init --src aks-dev-test.json --target custom.json
```

然后，您可以自定义配置文件中，通过手动编辑，也可以使用*mssqlctl 群集配置部分，设置*命令。 此 set 命令结合使用 jsonpath 和 jsonpatch 库来提供编辑配置文件的方法。

### <a name="configure-size"></a>配置大小

默认情况下，预配为每个群集中预配 pod 的永久性卷声明的大小为 10 GB。 可以更新此值以容纳在群集部署之前自定义配置文件中运行的工作负荷。

下面的示例仅更新存储池中的永久性卷声明的大小为 32 Gi:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.size=32Gi"
```

下面的示例更新为 32 Gi 的永久性卷声明所有池的大小：

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type[*])].spec.storage.size=32Gi"
```

### <a id="config-samples"></a> 配置存储类

下面的示例演示如何修改控制平面的存储类：

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.controlPlace.spec.storage.className=<yourStorageClassName>"
```

另一种方法是手动编辑自定义配置文件或更改存储池的存储类在以下示例中使用 jsonpatch 等。 创建*patch.json*文件使用以下内容：

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
        "replicas": 2,
        "type": "Storage",
        "storage": {
          "usePersistentVolume": true,
          "accessMode": "ReadWriteOnce",
          "className": "<yourStorageClassName>",
          "size": "32Gi"
        }
      }
    }
  ]
}
```

应用修补程序文件。 使用*mssqlctl 群集配置部分，设置*命令，将应用 JSON 修补程序文件中的更改。 下面的示例适用于目标部署配置文件 custom.json patch.json 文件。

```bash
mssqlctl cluster config section set -f custom.json -p ./patch.json
```

## <a name="next-steps"></a>后续步骤

有关在 Kubernetes 中的卷的完整文档，请参阅[卷上的 Kubernetes 文档](https://kubernetes.io/docs/concepts/storage/volumes/)。

有关部署 SQL Server 大数据群集的详细信息，请参阅[如何部署大数据群集在 Kubernetes 的 SQL Server](deployment-guidance.md)。

