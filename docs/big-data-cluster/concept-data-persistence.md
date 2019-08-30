---
title: Kubernetes 上的数据暂留
titleSuffix: SQL Server big data clusters
description: 了解数据暂留如何在 SQL Server 2019 大数据群集中运行。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7a12afd88f0eb83de7d5c5bd4a3735e71e037138
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155349"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Kubernetes 上的 SQL Server 大数据群集的数据暂留

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[持久卷](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)为 Kubernetes 中的存储提供了插件模型。 存储的提供方式是从其使用方式中抽象出来的。 因此，你可以提供自己的高可用性存储并将其插入到 SQL Server 大数据群集中。 这样，你便可完全控制所需的存储类型、可用性和性能。 Kubernetes 支持各种存储解决方案，包括 Azure 磁盘/文件、NFS、本地存储等。

## <a name="configure-persistent-volumes"></a>配置持久卷

SQL Server 大数据群集通过使用[存储类](https://kubernetes.io/docs/concepts/storage/storage-classes/)来使用这些持久卷。 可以为不同类型的存储创建不同的存储类，并在部署大数据群集时指定它们。 可以在池级别根据使用目的配置存储类和持久卷声明大小。 SQL Server 大数据群集为需要持久卷的每个组件创建具有指定存储类名的 [持久卷声明](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)。 然后，它将在 Pod 中装载相应的持久卷。 

## <a name="configure-big-data-cluster-storage-settings"></a>配置大数据群集存储设置

与其他自定义类似，可在部署时为每个池和控制平面在群集配置文件中指定存储设置。 如果池规范中没有存储配置设置，则将使用控制平面存储设置。 以下为存储配置部分的示例，可包含在规范中：

```json
    "storage": 
    {
      "data": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "15Gi"
      },
      "logs": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
    }
```

大数据群集的部署将使用持久存储来存储各种组件的数据、元数据和日志。 你可以自定义作为部署的一部分创建的持久卷声明的大小。 作为最佳做法，建议使用具有保留[回收策略](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)的存储类。

> [!NOTE]
> 在 CTP 3.2 中，无法在部署后修改存储配置设置。 此外，仅 `ReadWriteOnce` 支持整个群集的访问模式。

> [!WARNING]
> 在没有持久存储的情况下运行时可在测试环境中运行，但可能导致群集无法正常运行。 Pod 重启后，群集元数据和/或用户数据将永久丢失。 建议不要在此配置中运行。 

[配置存储](#config-samples)部分提供了有关如何为 SQL Server 大数据群集部署配置存储设置的更多示例。

## <a name="aks-storage-classes"></a>AKS 存储类

AKS 附带[两个内置存储类](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv)（default 和 managed-premium），以及这两个类的动态预配程序。 你可以指定其中一个，也可以创建自己的存储类来部署启用了持久存储的大数据群集。 默认情况下，用于 aks-dev-test 的内置群集配置文件附带使用“default”存储类的持久存储配置。

> [!WARNING]
> 使用内置存储类“default”和“managed premium”创建的持久卷包含回收策略“删除”。 因此，在删除 SQL Server 大数据群集时，持久卷声明会被删除，持久卷也会被删除。 可使用带有“保留”回收策略的 Azure 磁盘预配程序创建自定义存储类，如 [本文](https://docs.microsoft.com/azure/aks/concepts-storage#storage-classes)所示。


## <a name="minikube-storage-class"></a>Minikube 存储类

Minikube 附带一个名为“standard”的内置存储类以及该类的一个动态预配程序。 minikube minikube-dev-test 的内置配置文件具有控制平面规范中的存储配置设置。所有池规范都将应用相同的设置。 你还可以自定义此文件的副本，并将其用于 minikube 上的大数据群集部署。 可手动编辑自定义文件，并更改特定池的持久卷声明的大小，以适应要运行的工作负载。 或者，参阅[配置存储](#config-samples)部分，了解如何使用 azdata 命令进行编辑的示例。

## <a name="kubeadm-storage-classes"></a>Kubeadm 存储类

Kubeadm 没有内置存储类。 必须使用本地存储或首选预配程序（如 [Rook](https://github.com/rook/rook)）创建自己的存储类和持久卷。 在这种情况下，可以将“className”设置为配置的存储类。 

> [!NOTE]
>  在 kubeadm kubeadm-dev-test 的内置部署配置文件中，没有为数据和日志存储指定存储类名。 在部署之前，必须自定义配置文件并设置 className 的值，否则验证将失败。 部署还有一个验证步骤，用于检查存储类是否存在，但不是必需的持久卷。 必须确保根据群集的规模创建足够的卷。 在 CTP 3.1 中，对于默认群集大小，必须创建至少 23 个卷。 有关如何使用本地配置器创建持久卷的示例，请参阅[此处](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)。


## <a name="customize-storage-configurations-for-each-pool"></a>自定义每个池的存储配置

对于所有自定义项，必须首先创建要使用的内置配置文件的副本。 例如，下面的命令在名为 `custom` 的子目录中创建 aks-dev-test 部署配置文件的副本：

```bash
azdata bdc config init --source aks-dev-test --target custom
```

这会创建两个文件, 即**bdc**和**控件 json** , 可以通过手动编辑它们进行自定义, 也可以使用**azdata bdc config**命令。 可以结合使用 jsonpath 和 jsonpatch 库以提供编辑配置文件的方法。


### <a id="config-samples"></a> 配置存储类名称和/或声明大小

对于在群集中预配的每个 Pod，预配的持久卷声明的大小默认都是 10 GB。 可以在群集部署之前更新此值以适应你在自定义配置文件中运行的工作负载。

下面的示例将“control.jsaon”中持久卷声明大小的大小更新为 32Gi。 如果未在池级别重写，此设置将应用于所有池：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

下面的示例演示如何修改 control.json 文件的存储类：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

另一个选项是手动编辑自定义配置文件或使用 json 补丁，如下面的示例中所示，该补丁将更改存储池的存储类。 创建包含以下内容的 patch.json 文件：

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.resources.storage-0.spec",
      "value": {
        "type":"Storage",
        "replicas":2,
        "storage":{
            "data":{
                    "size": "100Gi",
                    "className": "myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    },
            "logs":{
                    "size":"32Gi",
                    "className":"myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    }
                }
            }
        }
    ]
}
```

应用补丁文件。 使用 azdata bdc config patch 命令应用 json 补丁文件中的更改。 下面的示例将 patch.json 文件应用于目标部署配置文件 custom.json。

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>后续步骤

有关 Kubernetes 中卷的完整文档，请参阅[有关卷的 Kubernetes文档](https://kubernetes.io/docs/concepts/storage/volumes/)。

有关部署 SQL Server 大数据群集的详细信息，请参阅[如何在 Kubernetes 上部署 SQL Server 大数据群集](deployment-guidance.md)。

