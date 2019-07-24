---
title: Kubernetes 上的数据暂留
titleSuffix: SQL Server big data clusters
description: 了解 SQL Server 2019 大数据群集中数据持久性的工作方式。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9142836032acc5e302c947e1619d17b07faff683
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419468"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Kubernetes 上的 SQL Server 大数据群集的数据持久性

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[永久性卷](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)为 Kubernetes 中的存储提供了一个插件模型。 如何将存储提供给其使用方式。 因此, 你可以使用自己的高度可用存储, 并将其插入 SQL Server 大数据群集。 这使你可以完全控制所需的存储、可用性和性能。 Kubernetes 支持多种存储解决方案, 包括 Azure 磁盘/文件、NFS、本地存储等。

## <a name="configure-persistent-volumes"></a>配置永久性卷

SQL Server 大数据群集使用这些永久性卷的方式是使用[存储类](https://kubernetes.io/docs/concepts/storage/storage-classes/)。 你可以为不同类型的存储创建不同的存储类, 并在大数据群集部署时间指定它们。 你可以配置要在池级别用于哪个用途的存储类和永久卷声明大小。 SQL Server 大数据群集使用指定的存储类名称为需要持久性卷的每个组件创建[永久性卷声明](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)。 然后, 它将在 pod 中装载相应的永久性卷。 

## <a name="configure-big-data-cluster-storage-settings"></a>配置大数据群集存储设置

与其他自定义类似, 你可以在部署时为每个池和控制面指定群集配置文件中的存储设置。 如果池规范中没有存储配置设置, 则将使用控制平面存储设置。 这是可在规范中包含的存储配置部分的示例:

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

大数据群集的部署将使用永久性存储来存储各种组件的数据、元数据和日志。 你可以自定义作为部署的一部分创建的永久性卷声明的大小。 作为最佳做法, 我们建议将存储类与*保留*[回收策略](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)配合使用。

> [!NOTE]
> 在 CTP 3.2 中, 无法修改部署后的存储配置设置。 此外, 仅`ReadWriteOnce`支持整个群集的访问模式。

> [!WARNING]
> 无持久存储的运行可以在测试环境中运行, 但这可能会导致不能正常运行的群集。 在 pod 重新启动时, 群集元数据和/或用户数据将永久丢失。 建议不要在此配置中运行。 

[配置存储](#config-samples)部分提供了有关如何为 SQL Server 大数据群集部署配置存储设置的更多示例。

## <a name="aks-storage-classes"></a>AKS 存储类

AKS 附带了[两个内置的存储类](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **,** 以及针对它们的动态配置程序。 你可以指定其中的任何一个, 或创建你自己的存储类, 以便部署大数据群集并启用持久存储。 默认情况下, aks *aks*的内置群集配置文件附带了用于使用**默认**存储类的持久存储配置。

> [!WARNING]
> 使用内置存储类创建的持久卷**默认**和**托管-高级版**具有*删除*的回收策略。 因此, 在删除 SQL Server 大数据群集时, 永久卷声明也会被删除, 然后也会永久删除。 如[本文中所](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes)示, 可以使用**azure 磁盘**privioner 和*保留*回收策略来创建自定义存储类。


## <a name="minikube-storage-class"></a>Minikube 存储类

Minikube 附带了一个名为**standard**的内置存储类和一个动态配置程序。 Minikube *minikube*的内置配置文件在控制平面规范中具有存储配置设置。这些设置将应用于所有池规范。 你还可以自定义此文件的副本, 并将其用于 minikube 上的大数据群集部署。 可以手动编辑自定义文件, 并更改特定池的永久性卷声明的大小, 以适应要运行的工作负荷。 或者, 有关如何使用*azdata*命令进行编辑的示例, 请参阅[配置存储](#config-samples)部分。

## <a name="kubeadm-storage-classes"></a>Kubeadm 存储类

Kubeadm 不附带内置的存储类。 必须使用本地存储或首选配置程序 (例如[车](https://github.com/rook/rook)) 创建自己的存储类和永久卷。 在这种情况下, 需要将类**名**设置为配置的存储类。 

> [!NOTE]
>  在*kubeadm kubeadm*的内置部署配置文件中, 没有为数据和日志存储指定存储类名称。 在部署之前, 必须自定义配置文件并设置 className 的值, 否则预先部署验证将失败。 部署还具有一个验证步骤, 用于检查存储类是否存在, 但不会检查所需的永久性卷。 必须确保根据群集的规模创建足够的卷。 在 CTP 3.1 中, 对于默认群集大小, 必须至少创建23个卷。 [下面](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)是有关如何使用本地配置程序创建持久卷的示例。


## <a name="customize-storage-configurations-for-each-pool"></a>为每个池自定义存储配置

对于所有自定义项, 首先必须创建要使用的内置配置文件的副本。 例如, 以下命令在名为`custom`的子目录中创建*aks-* ---

```bash
azdata bdc config init --source aks-dev-test --target custom
```

这会创建两个文件: **cluster**和**控件 json** , 可以通过手动编辑这些文件进行自定义, 也可以使用**azdata bdc config**命令。 可以结合使用 jsonpath 和 jsonpatch 库来提供编辑配置文件的方法。


### <a id="config-samples"></a>配置存储类名称和/或声明大小

默认情况下, 为群集中预配的每个 pod 预配的永久性卷声明大小为 10 GB。 在部署群集之前, 可以更新此值, 以适应在自定义配置文件中运行的工作负荷。

下面的示例将永久性卷声明大小的大小更新为**jsaon**中的32Gi。 如果在池级别未重写, 则此设置将应用于所有池:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

下面的示例演示如何修改**控件 json**文件的存储类:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

另一种方法是手动编辑自定义配置文件或使用 json 修补程序, 如以下示例中更改存储池的存储类。 使用以下内容创建一个*patch*文件:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage"
      "value": {
          "type":"Storage",
          "replicas":2,
          "data": {
            "className": "default",
            "accessMode": "ReadWriteOnce",
            "size": "100Gi"
          },
          "logs": {
            "className": "default",
            "accessMode": "ReadWriteOnce",
            "size": "32Gi"
          }
        }
      }
  ]
}
```

应用修补程序文件。 使用**azdata bdc config patch**命令应用 JSON 修补程序文件中的更改。 下面的示例将 patch 文件应用到目标部署配置文件自定义. json。

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>后续步骤

有关 Kubernetes 中的卷的完整文档, 请参阅[Kubernetes 文档](https://kubernetes.io/docs/concepts/storage/volumes/)。

有关部署 SQL Server 大数据群集的详细信息, 请参阅[如何在 Kubernetes 上部署 SQL Server 大数据群集](deployment-guidance.md)。

