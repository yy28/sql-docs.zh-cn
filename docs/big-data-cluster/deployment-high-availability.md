---
title: 部署高可用性 SQL Server 大数据群集
titleSuffix: Deploy SQL Server Big Data Cluster with high availability
description: 了解如何部署[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (预览版) 以实现高可用性。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2c0e5f5a5f194045b5d1b48a383f9d4dfd282649
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158162"
---
# <a name="deploy-sql-server-big-data-cluster-with-high-availability"></a>部署高可用性 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

部署大数据群集 (BDC) 时, 可以配置要在可用性组配置中部署 SQL Server 主节点。 此配置在 Kubernetes 基础结构通过其内置的运行状况监视、故障检测和故障转移机制的基础上提高了 SQL Server master 的可靠性。 可用性组 (AG) 将冗余添加到 SQL Server 的实例。 在此配置中, 监视、故障检测和故障转移任务由大数据群集管理服务 (即控制服务) 管理。

此外, 大数据群集平台提供了其他管理任务, 例如设置数据库镜像终结点、创建可用性组和将数据库添加到可用性组。

下面是可用性组启用的一些功能:

1. 如果在部署配置文件中指定了高可用性设置, 则将创建名`containedag`为的单个可用性组。 默认情况下`containedag`有三个副本, 包括 primary。 可用性组的所有 CRUD 操作都是在内部进行管理的。
1. 所有数据库将自动添加到可用性组, 包括`master`和。 `msdb` Polybase 配置数据库不包括在可用性组中, 因为它们包括特定于每个副本的实例级元数据。
1. 将自动设置外部终结点以连接到 AG 数据库。 此终结`master-svc-external`点扮演 AG 侦听器的角色。
1. 为辅助副本的只读连接设置了另一个外部终结点。 

# <a name="deploy"></a>部署

在可用性组中部署 SQL Server master:

1. `hadr`启用功能
1. 指定 AG 的副本数 (最小值为 3)
1. 配置为与只读辅助副本建立连接而创建的第二个外部终结点的详细信息

以下步骤演示了如何创建包含这些设置的修补程序文件, 以及如何将其`aks-dev-test`应用于或`kubeadm-dev-test`配置文件。 这些步骤将演练如何修补`aks-dev-test`配置文件以添加 HA 属性的示例。

1. `ha-patch.json`创建文件

    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.resources.master.spec",
          "value": {
            "type": "Master",
            "replicas": 3,
            "endpoints": [
              {
                "name": "Master",
                "serviceType": "LoadBalancer",
                "port": 31433
              },
              {
                "name": "MasterSecondary",
                "serviceType": "LoadBalancer",
                "port": 31436
              }
            ],
            "settings": {
              "sql": {
                "hadr.enabled": "true"
              }
            }
          }
        }
      ]
    }
    ```

1. 克隆你的目标配置文件

    ```bash
    azdata config init --source aks-dev-test --target custom-aks
    ```

1. 将修补程序文件应用于自定义配置文件

    ```bash
    azdata bdc config patch -c custom-aks/bdc.json --patch-file patch.json
    ```

## <a name="connect-to-sql-server-databases"></a>连接到 SQL Server 数据库

根据要对 SQL Server master 运行的工作负荷的类型, 可以连接到主副本以进行读写工作负荷, 或连接到辅助副本中只读类型的工作负荷的数据库。 下面是每种连接类型的大纲:

### <a name="connect-to-databases-on-the-primary-replica"></a>连接到主副本上的数据库

对于与主副本的连接, 请`sql-server-master`使用终结点。 此终结点也是 AG 的侦听器。 所有连接都在可用性组的上下文中。 例如, 使用此终结点的默认连接将导致连接到 AG 中`master`的数据库, 而不是 SQL Server 实例`master`数据库。

```bash
azdata bdc endpoint list -e sql-server-master -o table
```

`Description                           Endpoint             Name               Protocol`
`------------------------------------  -------------------  -----------------  ----------`
`SQL Server Master Instance Front-End  13.64.235.192,31433  sql-server-master  tds`

### <a name="connect-to-databases-on-the-secondary-replicas"></a>连接到辅助副本上的数据库

对于与辅助副本中数据库的只读连接, 请使用`sql-server-master-readonly`终结点。 此终结点的作用类似于所有辅助副本上的负载均衡器。 在连接字符串中提供用户数据库上下文。

```bash
azdata bdc endpoint list -e sql-server-master-readonly -o table
```

`Description                                    Endpoint            Name                        Protocol`
`---------------------------------------------  ------------------  --------------------------  ----------`
`SQL Server Master Readable Secondary Replicas  13.64.238.24,31436  sql-server-master-readonly  tds`

### <a id="instance-connect"></a>连接 SQL Server 实例

对于某些操作, 例如设置服务器级别配置或手动将数据库添加到可用性组 (如果数据库是使用还原工作流创建的), 则需要连接到实例。 若要提供此连接, 请公开外部终结点。 下面的示例演示如何公开此终结点, 然后将使用还原工作流创建的数据库添加到可用性组。

- 通过连接到`sql-server-master`终结点并运行以下内容来确定承载主副本的 pod:

    ```sql
    SELECT @@SERVERNAME
   ```

- 通过创建新的 Kubernetes 服务来公开外部终结点

    对于 kubeadm 群集, 请运行以下命令。 将`podName`替换为上一步返回的服务器的名称, `serviceName`将创建 Kubernetes 服务的首选名称, 并`namespaceName`将 * 替换为 BDC 群集的名称。

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=NodePort
    ```

    对于 aks 群集运行, 请运行相同的命令, 但创建的服务的类型将是`LoadBalancer`。 例如： 

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=LoadBalancer
    ```

    下面是针对 aks 运行此命令的示例, 其中承载主副本的 pod 是`master-0`:

    ```bash
    kubectl -n mssql-cluster expose pod master-0 --port=1533  --name=master-sql-0 --type=LoadBalancer
    ```

    获取创建的 Kubernetes 服务的 IP:

    ```bash
    kubectl get services -n <namespaceName>
    ```

> [!IMPORTANT]
> 作为最佳做法, 您应通过运行以下命令删除上面创建的 Kubernetes 服务进行清理:
>
>```bash
>kubectl delete svc master-sql-0 -n mssql-cluster
>```

- 将数据库添加到可用性组。

    对于要添加到 AG 的数据库, 必须在完整恢复模式下运行, 并且必须执行日志备份。 使用上面创建的 Kubernetes 服务中的 IP 并连接到 SQL Server 实例, 然后运行 TSQL 语句, 如下所示。

    ```sql
    ALTER DATABASE <databaseName> SET RECOVERY FULL;
    BACKUP DATABASE <databaseName> TO DISK='<filePath>'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE <databaseName>
    ```

    下面的示例添加了一个名`sales`为的数据库, 该数据库在实例上已还原:

    ```sql
    ALTER DATABASE sales SET RECOVERY FULL;
    BACKUP DATABASE sales TO DISK='/var/opt/mssql/data/sales.bak'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE sales
    ```

## <a name="known-limitations"></a>已知的限制

下面是大型数据群集中 SQL Server master 的可用性组的已知问题和限制:

- 作为工作流`CREATE DATABASE` `RESTORE`的结果而创建的数据库不会自动添加到可用性组。`CREATE DATABASE FROM SNAPSHOT` [连接到该实例](#instance-connect), 并手动将该数据库添加到可用性组。
- 运行的服务器配置设置之类的`sp_configure`某些操作需要与主实例建立连接。 不能使用相应的主终结点。 按照[说明](#instance-connect)连接到 SQL Server 实例, 然后运行`sp_configure`。
- 部署 BDC 时必须创建高可用性配置。 部署后, 无法启用可用性组的高可用性配置。

## <a name="next-steps"></a>后续步骤

- 有关在大数据群集部署中使用配置文件的详细信息, 请参阅[如何[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]在 Kubernetes 上部署](deployment-guidance.md#configfile)。
- 有关 SQL Server 可用性组功能的详细信息, 请参阅[Always On 可用性组概述 (SQL Server)](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-2017)。
