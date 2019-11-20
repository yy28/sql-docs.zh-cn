---
title: Kubernetes 上的数据暂留
titleSuffix: SQL Server big data clusters
description: 了解数据暂留如何在 SQL Server 2019 大数据群集中运行。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4671bc07dd21a769746257339ea7903e3dda4701
ms.sourcegitcommit: 385a907ed1de8fa7ada76260ea3f92583eb09238
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2019
ms.locfileid: "74063968"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Kubernetes 上的 SQL Server 大数据群集的数据暂留

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[持久卷](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)为 Kubernetes 中的存储提供了插件模型。 存储的提供方式是从其使用方式中抽象出来的。 因此，你可以提供自己的高可用性存储并将其插入到 SQL Server 大数据群集中。 这样，你便可完全控制所需的存储类型、可用性和性能。 Kubernetes 支持各种存储解决方案，包括 Azure 磁盘/文件、NFS、本地存储等。

## <a name="configure-persistent-volumes"></a>配置持久卷

SQL Server 大数据群集通过使用[存储类](https://kubernetes.io/docs/concepts/storage/storage-classes/)来使用这些持久卷。 可以为不同类型的存储创建不同的存储类，并在部署大数据群集时指定它们。 可以在池级别根据使用目的配置存储类和持久卷声明大小。 SQL Server 大数据群集为需要持久卷的每个组件创建具有指定存储类名的 [持久卷声明](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)。 然后，它将在 Pod 中装载相应的持久卷。 

下面是在为大数据群集计划存储配置时要考虑的一些重要方面：

- 要成功部署大数据群集，必须确保所需数量的持久卷可用。 如果要在 AKS 群集上部署，并且使用的是内置存储类（`default` 或 `managed-premium`）之一，则这些类支持对持久卷进行动态预配。 这意味着你无需预先创建持久卷，但必须确保 AKS 群集中可用的工作器节点可以附加尽可能多的磁盘，因为部署需要持久卷。 根据为工作器节点指定的 [VM 大小](/azure/virtual-machines/linux/sizes/)，每个节点可以附加一定数量的磁盘。 对于默认大小的群集（无高可用性），至少需要 24 个磁盘。 如果要启用高可用性或扩展任何池，则必须确保每个附加副本至少有两个持久卷，而不考虑要扩展的资源。

- 如果在配置中提供的存储类的存储配置程序不支持动态预配，则必须预先创建持久卷。 例如，`local-storage` 配置程序不启用动态预配。 有关如何在使用 `kubeadm` 部署的 Kubernetes 群集中执行此操作的信息，请参阅此[示例脚本](https://github.com/microsoft/sql-server-samples/tree/cu1-bdc/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)。

- 部署大数据群集时，可以将同一存储类配置为供群集中的所有组件使用。 但生产部署的最佳做法是，各种组件需要不同的存储配置，以适应各种大小或吞吐量的工作负载。 可以覆盖控制器中为每个 SQL Server 主实例、数据和存储池指定的默认存储配置。 本文提供了有关如何执行此操作的示例。

- 自 SQL Server 2019 CU1 发布后，无法在部署后修改存储配置设置。 这不仅包括修改每个实例的持久卷声明的大小，还包括不支持部署后的缩放操作。 因此，在大数据群集之前计划存储布局非常重要。

- 通过在 Kubernetes 上部署为容器化应用程序，并使用有状态集和持久存储等功能，Kubernetes 确保在出现运行状况问题时重启 Pod，并将其附加到同一持久存储。 但是，如果出现节点故障，并且必须在另一节点上重启 Pod，此时如果该存储是故障节点的本地存储，则会增加不可用性风险。 要克服这一风险，必须配置其他冗余并启用[高可用性功能](deployment-high-availability.md)，或者使用远程冗余存储。 下面概述了大数据群集中各种组件的存储选项。

| Resources | 数据存储类型 | 日志存储类型 |  说明 |
|---|---|---|--|
| SQL Server 主实例 | 本地（副本＞＝3）或远程冗余存储（副本＝1） | 本地存储 | 基于有状态集的实现（其中 Pod 固定在节点上）将确保重启和瞬时故障不会导致数据丢失。 |
| 计算池 | 本地存储* | 本地存储 | 未存储任何用户数据。 |
| 数据池 | 本地/远程冗余存储 | 本地存储 | 如果无法从其他数据源重建数据池，请使用远程冗余存储。  |
| 存储池 (HDFS) | 本地/远程冗余存储 | 本地存储 | 已启用 HDFS 复制。 |
| Spark 池 | 本地存储* | 本地存储 | 未存储任何用户数据。 |
| 控件（controldb、metricsd、logsdb）| 远程冗余存储 | 本地存储 | 对大数据群集元数据使用存储级冗余至关重要。 |

> [!IMPORTANT]
> 必须确保与控制相关的组件位于远程冗余存储上。 `controldb-0` Pod 使用数据库托管 SQL Server 实例，这些数据库存储有关群集服务状态、各种设置等的所有元数据。此实例不可用将导致群集中其他依赖服务出现运行状况问题。

## <a name="configure-big-data-cluster-storage-settings"></a>配置大数据群集存储设置

与其他自定义类似，可在部署时在群集配置文件中为 `bdc.json` 配置文件中的每个池和 `control.json` 文件中的控制服务指定存储设置。 如果池规范中没有存储配置设置，则控制存储设置将用于所有其他组件，包括 SQL Server 主实例（`master` 资源）、HDFS（`storage-0` 资源）或数据池。 以下为存储配置部分的示例，可包含在规范中：

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

大数据群集的部署将使用持久存储来存储各种组件的数据、元数据和日志。 你可以自定义作为部署的一部分创建的持久卷声明的大小。 作为最佳做法，建议使用具有保留[回收策略](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)的存储类  。

> [!WARNING]
> 在没有持久存储的情况下运行时可在测试环境中运行，但可能导致群集无法正常运行。 Pod 重启后，群集元数据和/或用户数据将永久丢失。 建议不要在此配置中运行。 

[配置存储](#config-samples)部分提供了有关如何为 SQL Server 大数据群集部署配置存储设置的更多示例。

## <a name="aks-storage-classes"></a>AKS 存储类

AKS 附带[两个内置存储类](/azure/aks/azure-disks-dynamic-pv/)（`default` 和 `managed-premium`），以及这两个类的动态预配程序。 你可以指定其中一个，也可以创建自己的存储类来部署启用了持久存储的大数据群集。 默认情况下，用于 `aks-dev-test` 的内置群集配置文件附带使用 `default` 存储类的持久存储配置。

> [!WARNING]
> 使用内置存储类 `default` 和 `managed-premium` 创建的持久卷包含回收策略“删除”  。 因此，在删除 SQL Server 大数据群集时，持久卷声明会被删除，持久卷也会被删除。 可使用带有 `Retain` 回收策略的 `azure-disk` 预配程序创建自定义存储类，如[本文](/azure/aks/concepts-storage/#storage-classes)所示。

## <a name="storage-classes-for-kubeadm-clusters"></a>`kubeadm` 群集的存储类 

使用 `kubeadm` 部署的 Kubernetes 群集没有内置的存储类。 必须使用本地存储或首选预配程序（如 [Rook](https://github.com/rook/rook)）创建自己的存储类和持久卷。 在这种情况下，可以将 `className` 设置为配置的存储类。 

> [!IMPORTANT]
>  在 kubeadm（`kubeadm-dev-test` 或 `kubeadm-prod`）的内置部署配置文件中，没有为数据和日志存储指定存储类名。 在部署之前，必须自定义配置文件并设置 `className` 的值，否则验证将失败。 部署还有一个验证步骤，用于检查存储类是否存在，但不是必需的持久卷。 必须确保根据群集的规模创建足够的卷。 对于默认的最小群集大小（默认规模，无高可用性），必须创建至少 24 个持久卷。
>
>[创建 Kubernetes 群集](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) 举例说明了如何使用本地配置程序创建永久性卷。 此示例介绍了 Kubernetes 存储。


## <a name="customize-storage-configurations-for-each-pool"></a>自定义每个池的存储配置

对于所有自定义项，必须首先创建要使用的内置配置文件的副本。 例如，下列命令在名为 `custom` 的子目录中创建 `aks-dev-test` 部署配置文件的副本：

```bash
azdata bdc config init --source aks-dev-test --target custom
```

这将创建两个文件，即 `bdc.json` 和 `control.json`，可以通过手动编辑这两个文件进行自定义，也可以使用 `azdata bdc config` 命令。 可以结合使用 jsonpath 和 jsonpatch 库以提供编辑配置文件的方法。


### <a id="config-samples"></a> 配置存储类名称和/或声明大小

对于在群集中预配的每个 Pod，预配的持久卷声明的大小默认都是 10 GB。 可以在群集部署之前更新此值以适应你在自定义配置文件中运行的工作负载。

下面的示例将 `control.json` 中持久卷声明大小的大小更新为 32Gi。 如果未在池级别重写，此设置将应用于所有池：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

下面的示例演示如何修改 `control.json` 文件的存储类：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

另一个选项是手动编辑自定义配置文件或使用 json 补丁，如下面的示例中所示，该补丁将更改存储池的存储类。 创建包含以下内容的 `patch.json` 文件：

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

应用补丁文件。 使用 `azdata bdc config patch` 命令应用 JSON 补丁文件中的更改。 下面的示例将 `patch.json` 文件应用到目标部署配置文件 `custom.json`。

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>后续步骤

有关 Kubernetes 中卷的完整文档，请参阅[有关卷的 Kubernetes文档](https://kubernetes.io/docs/concepts/storage/volumes/)。

有关部署 SQL Server 大数据群集的详细信息，请参阅[如何在 Kubernetes 上部署 SQL Server 大数据群集](deployment-guidance.md)。
