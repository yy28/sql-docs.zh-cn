---
title: 监视和故障排除
titleSuffix: SQL Server big data clusters
description: 本文提供了用于监视和解决 SQL Server 2019 大数据群集 (预览版) 的有用命令。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 272249b7bd6c22895b7d10e7fbce4a20cb647a49
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419480"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>SQL Server 大数据群集的监视和故障排除

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍可用于监视 SQL Server 2019 大数据群集 (预览版) 并对其进行故障排除的几个有用的 Kubernetes 命令。 其中介绍了如何查看位于大数据群集中的 pod 或其他 Kubernetes 项目的详细信息。 本文还介绍了一些常见的任务, 例如, 将文件复制到运行 SQL Server 大数据群集服务之一的容器。

> [!TIP]
> 在 Windows (cmd 或 PS) 或 Linux (bash) 客户端计算机上运行以下**kubectl**命令。 它们要求在群集中进行以前的身份验证, 并在其上运行群集上下文。 例如, 对于之前创建的 AKS 群集, 你可以运行`az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>`来下载 Kubernetes 群集配置文件并设置群集上下文。

## <a name="get-status-of-pods"></a>获取 pod 状态

可以使用`kubectl get pods`命令获取群集中所有命名空间或大数据群集命名空间的 pod 的状态。 以下部分显示了这两种情况的示例。

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>显示 Kubernetes 群集中所有盒的状态

运行以下命令以获取所有 pod 及其状态, 包括在中创建 SQL Server 大数据群集 pod 的命名空间中的 pod:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>显示 SQL Server 大数据群集中所有盒的状态

`-n`使用参数指定特定的命名空间。 请注意, 在基于部署配置文件中指定的群集名称在群集启动时创建的新命名空间中创建 SQL Server 大数据群集 pod。 此处使用默认名称`mssql-cluster`。

```bash
kubectl get pods -n mssql-cluster
```

对于正在运行的大数据群集, 你应看到类似于下面的输出:

```output
PS C:\> kubectl get pods -n mssql-cluster
NAME              READY   STATUS    RESTARTS   AGE
appproxy-f2qqt    2/2     Running   0          110m
compute-0-0       3/3     Running   0          110m
control-zlncl     4/4     Running   0          118m
data-0-0          3/3     Running   0          110m
data-0-1          3/3     Running   0          110m
gateway-0         2/2     Running   0          109m
logsdb-0          1/1     Running   0          112m
logsui-jtdnv      1/1     Running   0          112m
master-0          7/7     Running   0          110m
metricsdb-0       1/1     Running   0          112m
metricsdc-shv2f   1/1     Running   0          112m
metricsui-9bcj7   1/1     Running   0          112m
mgmtproxy-x6gcs   2/2     Running   0          112m
nmnode-0-0        1/1     Running   0          110m
storage-0-0       7/7     Running   0          110m
storage-0-1       7/7     Running   0          110m
```

> [!NOTE]
> 在部署期间, 仍然会出现**状态**为 " **ContainerCreating** " 的 pod。 如果出于任何原因而导致部署挂起, 这可以让你了解问题所在。 同时查看 "**就绪**" 列。 这会告知在 pod 中启动了多少个容器。 请注意, 部署可能需要30分钟或更长时间, 具体取决于你的配置和网络。 大多数情况下, 需要为不同组件下载容器映像。

## <a name="get-pod-details"></a>获取 pod 详细信息

运行以下命令以获取 JSON 格式输出中特定 pod 的详细说明。 它包括详细信息, 如 Kubernetes 上的当前 "" 节点、在 pod 中运行的容器, 以及用于启动容器的映像。 它还显示与该 pod 关联的其他详细信息, 例如标签、状态和持久化卷声明。

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

以下示例显示了一个名为`master-0` `mssql-cluster`的大数据群集中 pod 的详细信息:

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

如果发生了任何错误, 有时可能会在 pod 的最近事件中看到该错误。

## <a name="get-pod-logs"></a>获取 pod 日志

可以检索在 pod 中运行的容器的日志。 以下命令将检索在 pod `master-0`中运行的所有容器的日志, 并将其输出到`master-0-pod-logs.txt`文件名:

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluser > master-0-pod-logs.txt
```

## <a id="services"></a>获取服务的状态

运行以下命令以获取大数据群集服务的详细信息。 这些详细信息包括其类型和与相应服务和端口关联的 Ip。 请注意, SQL Server 大数据群集服务是在群集启动时基于部署配置文件中指定的群集名称创建的新命名空间中创建的。

```bash
kubectl get svc -n <namespace_name>
```

以下示例显示了一个名`mssql-cluster`为的大数据群集中服务的状态:

```bash
kubectl get svc -n mssql-cluster
```

以下服务支持到大数据群集的外部连接:

| 服务 | 描述 |
|---|---|
| **master-svc-external** | 提供对主实例的访问。<br/>(**外部 IP、31433**和**SA**用户) |
| **controller-svc-external** | 支持管理群集的工具和客户端。 |
| **gateway-svc-external** | 提供对 HDFS/Spark 网关的访问权限。<br/>(**外部 IP**和**根**用户) |
| **appproxy-svc-external** | 支持应用程序部署方案。 |

> [!TIP]
> 这是一种使用**kubectl**查看服务的方法, 但也可以使用`azdata bdc endpoint list`命令来查看这些终结点。 有关详细信息, 请参阅[获取大数据群集终结点](deployment-guidance.md#endpoints)。

## <a name="get-service-details"></a>获取服务详细信息

运行此命令可获取 JSON 格式输出中服务的详细说明。 它将包括标签、选择器、IP、外部 IP (如果服务为 LoadBalancer 类型)、端口等详细信息。

```bash
kubectl describe service <service_name> -n <namespace_name>
```

下面的示例检索**master-svc 外部**服务的详细信息:

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="run-commands-in-a-container"></a>在容器中运行命令

如果现有工具或基础结构不允许你执行特定任务, 而不是实际在容器的上下文中执行, 则可以使用`kubectl exec`命令登录到容器。 例如, 你可能需要检查是否存在特定的文件, 或者你可能需要重新启动容器中的服务。 

若要使用`kubectl exec`命令, 请使用以下语法:

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

以下两个部分提供了在特定容器中运行命令的两个示例。

### <a id="restartsql"></a>登录到特定容器并重新启动 SQL Server 进程

下面的示例演示如何在`mssql-server` `master-0` pod 中的容器中重新启动 SQL Server 进程:

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a>登录到特定容器并在容器中重新启动服务
 
下面的示例演示如何重新启动**supervisord**管理的所有服务: 

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl -c /opt/supervisor/supervisord.conf reload
```

## <a id="copy"></a>复制文件

如果需要将文件从容器复制到本地计算机, 请使用命令, `kubectl cp`并使用以下语法:

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

同样, 可以使用`kubectl cp`将文件从本地计算机复制到特定容器。

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a>从容器复制文件

下面的示例将 SQL Server 日志文件从容器复制到本地计算机`~/temp/sqlserverlogs`上的路径 (在本示例中, 本地计算机是 Linux 客户端):

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a>将文件复制到容器中

下面的示例将**AdventureWorks2016CTP3**文件从本地计算机复制到`mssql-server` `master-0` pod 中的 SQL Server 主实例容器 ()。 文件将被复制到容器`/tmp`中的目录。 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a>强制删除 pod
 
建议不要强制删除 pod。 但对于测试可用性、复原性或数据暂留, 可以使用`kubectl delete pods`命令删除 pod 来模拟 pod 故障。

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

以下示例删除存储池 pod `storage-0-0`:

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a>获取 pod IP
 
出于故障排除目的, 可能需要获取 pod 当前正在其上运行的节点的 IP。 若要获取 IP 地址, 请使用`kubectl get pods`具有以下语法的命令:

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

下面的示例获取运行`master-0` pod 的节点的 IP 地址:

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="kubernetes-dashboard"></a>Kubernetes 仪表板

可以启动 Kubernetes 仪表板, 获取有关群集的其他信息。 以下部分介绍了如何在 AKS 上启动 Kubernetes 的仪表板, 以及如何使用 kubeadm 引导 Kubernetes。
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>在 AKS 中运行群集时启动仪表板

若要启动 Kubernetes 仪表板, 请运行:

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> 如果收到以下错误:*无法在端口8001上侦听:由于以下错误, 无法创建所有侦听器:无法创建侦听器:错误侦听 tcp4 127.0.0.1: 8001: > 绑定:通常仅允许每个套接字地址 (协议/网络地址/端口) 的一次使用。无法创建侦听器:错误侦听 tcp6: address [[:: 1]]: 8001: > 地址中缺少端口错误:无法侦听任何请求的端口: [{8001 9090}]* , 请确保没有从另一个窗口中启动该仪表板。

当你在浏览器上启动仪表板时, 你可能会收到权限警告, 因为在 AKS 群集中默认启用了 RBAC, 并且该仪表板所使用的服务帐户没有足够的权限访问所有资源 (例如 *,禁止盒:用户 "system: serviceaccount: kube: kubernetes" 无法列出命名空间 "default"* 中的 pod。 运行以下命令`kubernetes-dashboard`, 为所需的权限, 然后重新启动仪表板:

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>使用 kubeadm 引导 Kubernetes 群集时启动仪表板

有关如何在 Kubernetes 群集中部署和配置仪表板的详细说明, 请参阅[Kubernetes 文档](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)。 若要启动 Kubernetes 仪表板, 请运行以下命令:

```bash
kubectl proxy
```

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息, 请参阅[什么是 SQL Server 大数据群集](big-data-cluster-overview.md)。
