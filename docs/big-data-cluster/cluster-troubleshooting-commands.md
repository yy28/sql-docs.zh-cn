---
title: 监视和故障排除
titleSuffix: SQL Server big data clusters
description: 本文提供了用于监视和故障排除 SQL Server 2019 大数据群集 （预览版） 的有用命令。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 3914bc088ab8974c92a24131d69590b4353f068e
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994082"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>监视和故障排除 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍可用于监视和故障排除 SQL Server 2019 大数据群集 （预览版） 的多个有用的 Kubernetes 命令。 它演示如何查看 pod 或位于大数据群集中其他 Kubernetes 项目的深入详细信息。 本文还介绍了常见任务，如将文件复制到或从运行 SQL Server 大数据群集服务之一的容器。

> [!TIP]
> 运行以下**kubectl** （cmd 或 PS） 的 Windows 或 Linux (bash) 客户端计算机上的命令。 它们需要在群集和群集上下文，针对运行中的上一个身份验证。 例如，对于以前创建的 AKS 群集，可以运行`az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>`下载 Kubernetes 群集配置文件和设置的群集上下文。

## <a name="get-status-of-pods"></a>获取 pod 的状态

可以使用`kubectl get pods`命令获得的所有命名空间或大数据群集命名空间的群集中的 pod 的状态。 以下部分说明这两者的示例。

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>在 Kubernetes 群集中显示的所有 pod 的状态

运行以下命令以获取所有 pod 和及其状态，包括 pod 的命名空间部分的 SQL Server 中创建大数据群集 pod:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>在 SQL Server 大数据群集中显示的所有 pod 的状态

使用`-n`参数来指定特定的命名空间。 请注意，在根据部署配置文件中指定的群集名称群集启动时创建的新命名空间中创建 SQL Server 大数据群集 pod。 默认名称， `mssql-cluster`，此处使用。

```bash
kubectl get pods -n mssql-cluster
```

应看到类似于下面的列表，用于运行大数据群集的输出：

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
> 在部署期间，使用的 pod**状态**的**ContainerCreating**仍即将推出。 如果部署出于任何原因挂起，它可以了解该问题可能是。 此外介绍**准备**列。 这将告知你多少个容器已开始在 pod 中。 请注意，部署可能需要 30 分钟或更具体取决于你的配置和网络。 其中大部分时间都花下载不同组件的容器映像。

## <a name="get-pod-details"></a>获取 pod 的详细信息

运行以下命令以获取 JSON 格式输出中的特定 pod 的详细的说明。 它包括详细信息，例如当前放置在 pod，在 pod 和用于启动容器的映像中运行的容器的 Kubernetes 节点。 它还显示其他详细信息，例如标签，状态，并保留卷声明所带来的 pod。

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

下面的示例显示的详细信息`master-0`中名为的大数据群集的 pod `mssql-cluster`:

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

如果发生了任何错误，您有时可以看到 pod 的新事件中的错误。

## <a name="get-pod-logs"></a>获取 pod 日志

您可以检索一个 pod 中运行的容器的日志。 以下命令将检索名为在 pod 中运行的所有容器的日志`master-0`，并输出到文件名称`master-0-pod-logs.txt`:

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluser > master-0-pod-logs.txt
```

## <a id="services"></a> 获取服务状态

运行以下命令以获取大数据群集服务的详细信息。 这些详细信息包括它们的类型和 Ip 与相应的服务和端口相关联。 请注意，在根据部署配置文件中指定的群集名称群集启动时创建的新命名空间中创建 SQL Server 大数据群集服务。

```bash
kubectl get svc -n <namespace_name>
```

下面的示例演示服务的状态中名为的大数据群集`mssql-cluster`:

```bash
kubectl get svc -n mssql-cluster
```

以下服务支持大数据群集的外部连接：

| 服务 | Description |
|---|---|
| **master-svc-external** | 可以访问主实例。<br/>(**外部 IP，31433**并**SA**用户) |
| **controller-svc-external** | 支持工具和管理群集的客户端。 |
| **mgmtproxy-svc-external** | 提供对访问[群集管理门户](cluster-admin-portal.md)。<br/>(https://**外部 IP**: 30777/门户) |
| **gateway-svc-external** | 提供对 HDFS/Spark 网关的访问。<br/>(**EXTERNAL-IP**并**根**用户) |
| **appproxy-svc-external** | 支持应用程序部署方案。 |

> [!TIP]
> 这是一种方法查看与服务**kubectl**，但也可以使用`mssqlctl cluster endpoint list`命令来查看这些终结点。 有关详细信息，请参阅[获取大数据群集终结点](deployment-guidance.md#endpoints)。

## <a name="get-service-details"></a>获取服务详细信息

运行此命令可获取 JSON 格式输出中的一项服务的详细的说明。 它将包含详细信息如标签、 选择器中，IP、 外部 IP （如果该服务的负载均衡器类型）、 端口，等等。

```bash
kubectl describe service <service_name> -n <namespace_name>
```

下面的示例检索的详细信息**master svc 外部**服务：

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="run-commands-in-a-container"></a>在容器中运行的命令

如果现有的工具或基础结构不会启用你实际上并不具有在容器的上下文中执行某项任务，你可以登录到容器使用`kubectl exec`命令。 例如，您可能需要检查是否存在某个特定文件，或可能需要重新启动服务，容器中。 

若要使用`kubectl exec`命令，请使用以下语法：

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

以下两个部分提供在特定容器中运行命令的两个示例。

### <a id="restartsql"></a> 登录到特定容器并重新启动 SQL Server 进程

下面的示例演示如何重新启动 SQL Server 进程中的`mssql-server`容器中的`master-0`pod:

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a> 登录到特定容器并在容器中重新启动服务
 
下面的示例演示如何重新启动所有服务由**进行**: 

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl -c /opt/supervisor/supervisord.conf reload
```

## <a id="copy"></a> 将文件复制

如果你需要将文件从容器复制到本地计算机，使用`kubectl cp`命令使用以下语法：

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

同样，可以使用`kubectl cp`将文件从本地计算机复制到特定容器中。

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a> 从容器复制文件

以下示例将 SQL Server 日志文件复制到容器中`~/temp/sqlserverlogs`（在此示例在本地计算机是 Linux 客户端） 在本地计算机上的路径：

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a> 将文件复制到容器

下面的示例副本**将 AdventureWorks2016CTP3.bak**文件中的从本地计算机到 SQL Server 主实例容器 (`mssql-server`) 中`master-0`pod。 将文件复制到`/tmp`目录容器中。 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a> 强制删除一个 pod
 
建议不要以强制删除一个 pod。 但对于测试可用性、 复原能力或数据持久性，您可以删除 pod 以模拟 pod 故障`kubectl delete pods`命令。

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

以下示例将删除存储池 pod， `storage-0-0`:

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a> 获取 pod IP
 
有关故障排除目的，可能需要获取的节点当前运行 pod IP。 若要获取的 IP 地址，请使用`kubectl get pods`命令使用以下语法：

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

下面的示例获取节点的 IP 地址`master-0`上运行 pod:

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="cluster-administration-portal"></a>群集管理门户

使用[群集管理门户](cluster-admin-portal.md)来监视大数据群集的状态。 例如，在部署中，您可以使用**部署**选项卡。你必须等待**mgmtproxy svc 外部**要访问此门户中，因此不会在部署开始之前启动服务。

## <a name="kubernetes-dashboard"></a>Kubernetes 仪表板

您可以启动 Kubernetes 仪表板有关群集的其他信息。 以下各节说明如何在 AKS 上的 kubernetes 和适用于 Kubernetes 引导使用 kubeadm 启动仪表板。
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>在 AKS 中运行群集时启动仪表板

若要启动 Kubernetes 仪表板运行：

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> 如果收到以下错误：*无法侦听端口 8001:所有侦听器都未能创建具有以下错误：无法创建侦听器：错误侦听 tcp4 127.0.0.1:8001: > 绑定：通常情况下允许的每个套接字地址 （协议/网络地址/端口） 只有一个使用情况。无法创建侦听器：错误侦听 tcp6： 地址 [[:: 1]]: 8001： 缺少中的端口 > 解决错误：无法在任何请求的端口上侦听: [{8001 9090}]*，请确保您没有启动仪表板已从另一个窗口。

在浏览器上启动仪表板中，可能会由于在 AKS 群集中，默认情况下启用的 RBAC 权限警告和仪表板使用的服务帐户没有足够的权限访问的所有资源时 (例如， *禁止 pod:用户"系统： serviceaccount:kube-系统： kubernetes 的仪表板"无法列出命名空间"default"中的 pod*)。 运行以下命令，为提供必要的权限来`kubernetes-dashboard`，然后重新启动仪表板：

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>在 Kubernetes 群集使用 kubeadm 引导时启动仪表板

有关详细说明如何部署和配置在 Kubernetes 群集中的仪表板，请参阅[Kubernetes 文档](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)。 若要启动 Kubernetes 仪表板，请运行以下命令：

```bash
kubectl proxy
```

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 SQL Server 大数据群集](big-data-cluster-overview.md)。
