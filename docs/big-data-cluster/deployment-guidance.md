---
title: 如何部署
titleSuffix: SQL Server big data clusters
description: 了解如何将部署在 Kubernetes 上的 SQL Server 2019 大数据群集 （预览版）。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 7a863259a3eb04aef648d98f1d8c4ac22e4a3f38
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582410"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>如何部署 SQL Server 大数据群集在 Kubernetes 上

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 大数据群集可部署为 docker 容器的 Kubernetes 群集上。 这是安装和配置步骤概述：

- 设置单个 VM 的 Vm，或在 Azure Kubernetes 服务 (AKS) 群集上的 Kubernetes 群集。
- 安装群集配置工具**mssqlctl**在客户端计算机上。
- 部署 Kubernetes 群集中的 SQL Server 大数据群集。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="prereqs"></a> Kubernetes 群集的先决条件

SQL Server 大数据群集至少需要版本最低为 Kubernetes 的 v1.10 服务器和客户端 (kubectl)。

> [!NOTE]
> 请注意，客户端和服务器的 Kubernetes 版本应 + 1 或-1 的次要版本。 有关详细信息，请参阅[Kubernetes 支持的版本和组件倾斜](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)。

## <a id="kubernetes"></a> Kubernetes 群集设置

如果已有的 Kubernetes 群集，满足上述先决条件，则您可以直接跳到[部署步骤](#deploy)。 本部分假定基本了解 Kubernetes 概念。  有关 Kubernetes 的详细信息，请参阅[Kubernetes 文档](https://kubernetes.io/docs/home)。

您可以选择部署在三种方式中的 Kubernetes:

| 部署 Kubernetes 上： | Description | 链接 |
|---|---|---|
| **Minikube** | 在 VM 中的单节点 Kubernetes 群集。 | [说明](deploy-on-minikube.md) |
| **Azure Kubernetes 服务 (AKS)** | Azure 中的托管的 Kubernetes 容器服务。 | [说明](deploy-on-aks.md) |
| **多台计算机** | 物理计算机或使用虚拟机上部署的 Kubernetes 群集**kubeadm** | [说明](deploy-with-kubeadm.md) |
  
> [!TIP]
> 部署 AKS 和 SQL Server 大数据群集的示例 python 脚本，请参阅[部署大数据群集在 Azure Kubernetes 服务 (AKS) SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks)。

## <a name="deploy-sql-server-2019-big-data-tools"></a>部署 SQL Server 2019 大数据工具

首次部署 SQL Server 2019 大数据群集之前[安装的大数据工具](deploy-big-data-tools.md):
- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 扩展**

## <a id="deploy"></a> 部署 SQL Server 大数据群集

配置在 Kubernetes 群集后，你可以继续进行 SQL Server 大数据群集的部署。 

> [!NOTE]
> 如果要从以前的版本进行升级，请参阅[升级部分中的](#upgrade)。

若要部署的开发/测试环境的所有默认配置与 Azure 中的大数据群集，请按照本文中的说明操作：

[快速入门：部署 SQL Server 大数据群集在 Kubernetes 上](quickstart-big-data-cluster-deploy.md)

如果你想要自定义根据工作负荷的大数据群集的部署需求，请按照本文的其余部分中的说明进行操作。

## <a name="verify-kubernetes-configuration"></a>验证 kubernetes 配置

运行**kubectl**命令以查看群集配置。 请确保该 kubectl 指向正确的群集上下文。

```bash
kubectl config view
```

## <a id="env"></a> 定义环境变量

可以使用一组环境变量传递给自定义群集配置`mssqlctl create cluster`命令。 环境变量的大部分都是可选的 with 根据下面的默认值。 请注意，环境变量，例如需要用户输入的凭据。

| 环境变量 | Required | 默认值 | Description |
|---|---|---|---|
| **ACCEPT_EULA** | 是 | 不可用 | 接受 SQL Server 许可协议 （例如，是）。  |
| **CLUSTER_NAME** | 是 | 不可用 | 要部署大数据群集到 SQLServer 的 Kubernetes 命名空间的名称。 |
| **CLUSTER_PLATFORM** | 是 | 不可用 | 部署 Kubernetes 群集的平台。 可以是`aks`， `minikube`， `kubernetes`|
| **CLUSTER_COMPUTE_POOL_REPLICAS** | 否 | 1 | 计算池副本来构建数。在 ctp 版本 2.4 仅值允许为 1。 |
| **CLUSTER_DATA_POOL_REPLICAS** | 否 | 2 | 池中的副本，以生成数据的数目。 |
| **CLUSTER_STORAGE_POOL_REPLICAS** | 否 | 2 | 存储池的副本，以生成数。 |
| **DOCKER_REGISTRY** | 是 | TBD | 用于部署群集的映像的存储位置的专用注册表。 |
| **DOCKER_REPOSITORY** | 是 | TBD | 专用存储库中的上述注册表存储映像。  它是必需的封闭的公共预览版的持续时间。 |
| **DOCKER_USERNAME** | 是 | 不可用 | 用于访问容器映像，以防在专用存储库中存储的用户名。 它是必需的封闭的公共预览版的持续时间。 |
| **DOCKER_PASSWORD** | 是 | 不可用 | 用于访问上述的专用存储库的密码。 它是必需的封闭的公共预览版的持续时间。|
| **DOCKER_EMAIL** | 是 | 不可用 | 你的电子邮件地址。 |
| **DOCKER_IMAGE_TAG** | 否 | 最新 | 用于标记图像的标签。 |
| **DOCKER_IMAGE_POLICY** | 否 | 始终 | 始终强制的映像拉取。  |
| **DOCKER_PRIVATE_REGISTRY** | 是 | 不可用 | 封闭的公共预览版的时间范围内，你必须设置此值设置为"1"。 |
| **CONTROLLER_USERNAME** | 是 | 不可用 | 对于群集管理员用户名。 |
| **CONTROLLER_PASSWORD** | 是 | 不可用 | 群集管理员的密码。 |
| **KNOX_PASSWORD** | 是 | 不可用 | Knox 用户的密码。 |
| **MSSQL_SA_PASSWORD** | 是 | 不可用 | 对于 master 的 SQL 实例 SA 用户的密码。 |
| **USE_PERSISTENT_VOLUME** | 否 | true | `true` 若要使用 Kubernetes 永久性卷声明 pod 存储。  `false` 使用临时主机存储为 pod 存储。 请参阅[数据暂留](concept-data-persistence.md)一文，了解更多详细信息。 如果部署在 minikube 的大数据群集的 SQL Server 和 USE_PERSISTENT_VOLUME = true，必须设置的值为`STORAGE_CLASS_NAME=standard`。 |
| **STORAGE_CLASS_NAME** | 否 | 默认值 | 如果`USE_PERSISTENT_VOLUME`是`true`这指示要使用的 Kubernetes 存储类的名称。 请参阅[数据暂留](concept-data-persistence.md)一文，了解更多详细信息。 如果部署在 minikube 的大数据群集的 SQL Server 时，默认的存储类名称不同，您必须通过设置重写此`STORAGE_CLASS_NAME=standard`。 |
| **CONTROLLER_PORT** | 否 | 30080 | 控制器服务在公共网络进行侦听 TCP/IP 端口。 |
| **MASTER_SQL_PORT** | 否 | 31433 | 主 SQL 实例在公用网络进行侦听 TCP/IP 端口。 |
| **KNOX_PORT** | 否 | 30443 | Apache Knox 在公用网络进行侦听 TCP/IP 端口。 |
| **PROXY_PORT** | 否 | 30777 | 代理服务在公共网络侦听 TCP/IP 端口。 这是用于计算在门户的端口的 URL。 |
| **GRAFANA_PORT** | 否 | 30888 | 监视应用程序 Grafana 在公用网络进行侦听 TCP/IP 端口。 |
| **KIBANA_PORT** | 否 | 30999 | Kibana 日志搜索应用程序在公用网络进行侦听 TCP/IP 端口。 |


> [!IMPORTANT]
>1. 受限个人预览版期间，专用 Docker 注册表的凭据将向您提供在会审您[EAP 注册](https://aka.ms/eapsignup)。
>1. 对于使用内置的本地群集**kubeadm**，环境变量的值`CLUSTER_PLATFORM`是`kubernetes`。 此外，当`USE_PERSISTENT_VOLUME=true`，必须预先预配 Kubernetes 存储类并将其传递通过使用`STORAGE_CLASS_NAME`。
>1. 请确保你在双引号内包装密码，如果它包含任何特殊字符。 您可以设置 MSSQL_SA_PASSWORD 为您希望的任何内容，但请确保它们是足够复杂并且不使用`!`，`&`或`'`字符。 请注意，双引号分隔符仅适用于 bash 命令。
>1. 群集的名称必须仅小写字母数字字符，不留空格。 将在具有与群集相同的名称的命名空间中创建群集的所有 Kubernetes 项目 （容器、 pod、 有状态集、 服务） 指定的名称。
>1. **SA**帐户是在安装过程中创建的 SQL Server 主实例上的系统管理员。 创建 SQL Server 容器，你指定的 MSSQL_SA_PASSWORD 环境变量是可发现通过运行后回显 $MSSQL_SA_PASSWORD 容器中。 出于安全考虑，更改 SA 密码根据最佳实践[此处](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password)。

根据使用的 Windows 或 Linux 客户端设置部署大数据群集所需的环境变量不同。  选择以下步骤使用具体取决于哪个操作系统。

初始化以下环境变量，它们所需的部署群集：

### <a name="windows"></a>Windows

使用 CMD 窗口 (而不是 PowerShell)，配置以下环境变量。 不要使用引号将值。

```cmd
SET ACCEPT_EULA=yes
SET CLUSTER_PLATFORM=<minikube or aks or kubernetes>

SET CONTROLLER_USERNAME=<controller_admin_name - can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password - can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password - can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username, credentials provided by Microsoft>
SET DOCKER_PASSWORD=<your password, credentials provided by Microsoft>
SET DOCKER_EMAIL=<your email address>
SET DOCKER_PRIVATE_REGISTRY=1
```

### <a name="linux"></a>Linux

初始化以下环境变量。 在 bash 中，可以使用引号将每个值。

```bash
export ACCEPT_EULA="yes"
export CLUSTER_PLATFORM="<minikube or aks or kubernetes>"

export CONTROLLER_USERNAME="<controller_admin_name - can be anything>"
export CONTROLLER_PASSWORD="<controller_admin_password - can be anything, password complexity compliant>"
export KNOX_PASSWORD="<knox_password - can be anything, password complexity compliant>"
export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

export DOCKER_REGISTRY="private-repo.microsoft.com"
export DOCKER_REPOSITORY="mssql-private-preview"
export DOCKER_USERNAME="<your username, credentials provided by Microsoft>"
export DOCKER_PASSWORD="<your password, credentials provided by Microsoft>"
export DOCKER_EMAIL="<your email address>"
export DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="minikube-settings"></a>Minikube 设置

如果要部署在 minikube 上并`USE_PERSISTENT_VOLUME=true`（默认值），您还必须重写的默认值为`STORAGE_CLASS_NAME`环境变量。

Minikube 部署在 Windows 上使用以下命令：

```cmd
SET STORAGE_CLASS_NAME=standard
```

Minikube 部署，在 Linux 上使用以下命令：

```bash
export STORAGE_CLASS_NAME=standard
```

或者，您可以禁止显示在 minikube 上通过设置使用永久性卷`USE_PERSISTENT_VOLUME=false`。

### <a name="kubadm-settings"></a>Kubadm 设置

如果使用 kubeadm 物理或虚拟机上进行部署，必须预先预配 Kubernetes 存储类并将其传递通过使用`STORAGE_CLASS_NAME`。 或者，您可以禁止显示通过设置使用永久性卷`USE_PERSISTENT_VOLUME=false`。 有关持久性存储区的详细信息，请参阅[与大数据群集在 Kubernetes 的 SQL Server 数据暂留](concept-data-persistence.md)。

## <a name="deploy-sql-server-big-data-cluster"></a>部署 SQL Server 大数据群集

创建群集 API 用于初始化 Kubernetes 命名空间并将其部署到该命名空间的所有应用程序 pod。 若要部署 Kubernetes 群集上的 SQL Server 大数据群集，请运行以下命令：

```bash
mssqlctl cluster create --name <your-cluster-name>
```

在群集启动期间客户端命令窗口将输出的部署状态。 在部署过程中，您应看到一系列消息，它正在等待控制器 pod:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

10 到 20 分钟后，您应会收到通知，正在运行的控制器 pod:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> 整个部署可能需要很长时间由于下载的大数据群集组件的容器映像所需的时间。 但是，也不会花费几个小时。 如果遇到你的部署的问题，请参阅[故障排除](#troubleshoot)本文，了解如何监视和检查部署的一部分。

部署完成后，输出会通知您成功：

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

## <a id="masterip"></a> 获取大数据群集终结点

部署脚本已成功完成后，可以获取如下所述的步骤的 SQL Server 主实例的 IP 地址。 将使用此 IP 地址和端口号 31433 连接到 SQL Server 主实例 (例如：  **\<ip-address-of-endpoint-master-pool\>、 31433**)。 同样，可以连接到 SQL Server 与大数据群集 （HDFS/Spark 网关） IP 相关联**终结点安全**服务。

下面的 kubectl 命令检索大数据群集的公共终结的点：

```bash
kubectl get svc endpoint-master-pool -n <your-cluster-name>
kubectl get svc endpoint-security -n <your-cluster-name>
kubectl get svc endpoint-service-proxy -n <your-cluster-name>
```

寻找**外部 IP**分配给每个服务的值。

中也概述了群集的所有终结点**服务终结点**群集管理门户中的选项卡。 您可以访问在门户中使用的外部 IP 地址和端口号`endpoint-service-proxy`(例如： **https://\<ip-address-of-endpoint-service-proxy\>: 30777/门户**)。 凭据的访问管理门户中的值`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`上面提供的环境变量。 此外可以使用群集管理门户来监视部署。

有关如何连接的详细信息，请参阅[连接到 SQL Server 大数据群集使用 Azure Data Studio](connect-to-big-data-cluster.md)。

### <a name="minikube"></a>Minikube

如果使用 Minikube，您需要运行以下命令来获取 IP 地址连接到所需。 除了 IP，指定您需要连接到终结点的端口。 若要获取的所有服务终结点 

```bash
minikube ip
```

不管平台如何在 Kubernetes 群集上运行，若要获取针对的群集，运行以下命令部署的所有服务终结点：
```bash
kubectl get svc -n <your-cluster-name>
```

## <a id="upgrade"></a> 升级到新版本

目前，大数据群集升级到新版本的唯一方法是手动删除并重新创建群集。 每个版本具有的唯一版本**mssqlctl**不是与以前的版本兼容。 此外，如果旧群集必须下载一个新的节点上的图像，最新的映像不可能与在群集上的较旧映像兼容。 若要升级到最新版本，请使用以下步骤：

1. 在删除之前在旧群集，备份数据，和 HDFS 上的 SQL Server 主实例。 对于 SQL Server 主实例，可以使用[SQL Server 备份和还原](data-ingestion-restore-database.md)。 Hdfs，你[可以在使用数据复制**curl**](data-ingestion-curl.md)。

1. 删除与旧群集`mssqlctl delete cluster`命令。

   ```bash
    mssqlctl cluster delete --name <old-cluster-name>
   ```

   > [!Important]
   > 使用的版本**mssqlctl**匹配你的群集。 不删除较旧群集使用的较新版本**mssqlctl**。

1. 卸载的任何旧版本**mssqlctl**。

   ```bash
   pip3 uninstall mssqlctl
   ```

   > [!IMPORTANT]
   > 不应安装的新版本**mssqlctl**而无需先卸载任何较旧版本。

1. 安装最新版本**mssqlctl**。 

   **Windows:**

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.4/mssqlctl/requirements.txt
   ```

   **Linux:**

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.4/mssqlctl/requirements.txt --user
   ```

   > [!IMPORTANT]
   > 对于每个版本的路径**mssqlctl**更改。 即使你安装了**mssqlctl**，则必须重新安装最新的路径中创建新群集之前。

1. 安装最新版本中的说明[部署部分](#deploy)的这篇文章。 

## <a id="troubleshoot"></a> 监视和故障排除

若要监视或排查部署问题，请使用**kubectl**检查群集的状态以及检测到潜在问题。 在部署期间，随时可以打开不同的命令窗口运行以下测试。

1. 检查你的群集中的 pod 的状态。

   ```cmd
   kubectl get pods -n <your-cluster-name>
   ```

   在部署期间，使用的 pod**状态**的**ContainerCreating**仍即将推出。 如果部署出于任何原因挂起，它可以了解该问题可能是。 此外介绍**准备**列。 这将告知你多少个容器已开始在 pod 中。 请注意，部署可能需要 30 分钟或更具体取决于你的配置和网络。 其中大部分时间都花下载不同组件的容器映像。 下表显示在部署过程中的两个容器的编辑的示例输出：

   ```output
   PS C:\> kubectl get pods -n sbdc8
   NAME                                     READY   STATUS              RESTARTS   AGE
   mssql-controller-h79ft                   4/4     Running             0          13m
   mssql-storage-pool-default-0             0/7     ContainerCreating   0          6m
   ```

1. 介绍了更多详细信息的单个 pod。 以下命令将检查`mssql-storage-pool-default-0`pod。

   ```cmd
   kubectl describe pod mssql-storage-pool-default-0 -n <your-cluster-name>
   ```

   这将输出有关 pod，其中包括最新事件的详细的信息。 如果出现错误，有时可找到以下的错误。

1. 检索一个 pod 中运行的容器的日志。 以下命令将检索名为在 pod 中运行的所有容器的日志`mssql-storage-pool-default-0`，并输出到文件名称`pod-logs.txt`:

   ```cmd
   kubectl logs mssql-storage-pool-default-0 --all-containers=true -n <your-cluster-name> > pod-logs.txt
   ```

1. 查看群集服务期间和之后在部署中使用以下命令：

   ```cmd
   kubectl get svc -n <your-cluster-name>
   ```

   这些服务支持与大数据群集内部和外部连接。 对于外部连接，则使用以下服务：

   | 服务 | Description |
   |---|---|
   | **endpoint-master-pool** | 可以访问主实例。<br/>(**外部 IP，31433**并**SA**用户) |
   | **endpoint-controller** | 支持工具和管理群集的客户端。 |
   | **endpoint-service-proxy** | 提供对访问[群集管理门户](cluster-admin-portal.md)。<br/>(https://**外部 IP**: 30777/门户)|
   | **endpoint-security** | 提供对 HDFS/Spark 网关的访问。<br/>(**EXTERNAL-IP**并**根**用户) |

1. 使用[群集管理门户](cluster-admin-portal.md)上监视部署**部署**选项卡。你必须等待**终结点服务代理**要访问此门户中，因此不会在部署开始之前启动服务。

> [!TIP]
> 有关群集进行疑难解答的详细信息，请参阅[Kubectl 命令进行监视和故障排除 SQL Server 大数据群集](cluster-troubleshooting-commands.md)。

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 大数据群集的详细信息，请参阅以下资源：

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
- [研讨会：Microsoft SQL Server 大数据群集体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)