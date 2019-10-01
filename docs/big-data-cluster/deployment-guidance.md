---
title: 部署指南
titleSuffix: SQL Server big data clusters
description: 了解如何在 Kubernetes [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]上部署（预览版）。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 66aeb6b6e13de8cc076d2ff1b4c77d4fadf2b94a
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688314"
---
# <a name="how-to-deploy-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-kubernetes"></a>如何在 Kubernetes [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上部署

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 大数据群集在 Kubernetes 群集上部署为 docker 容器。 下面概述了设置和配置步骤：

- 在单个 VM、VM 群集或 Azure Kubernetes 服务 (AKS) 中设置 Kubernetes 群集。
- 在自己的客户端计算机上安装群集配置工具 azdata。
- 在 Kubernetes 群集中部署 SQL Server 大数据群集。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>安装 SQL Server 2019 大数据工具

请先[安装大数据工具](deploy-big-data-tools.md)，然后再部署 SQL Server 2019 大数据群集：

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 扩展**

## <a id="prereqs"></a> Kubernetes 必备条件

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]对于服务器和客户端（kubectl），至少需要具有最低版本的 Kubernetes 版本。

> [!NOTE]
> 请注意，客户端和服务器 Kubernetes 版本应在 +1 或 -1 次要版本之内。 有关详细信息，请参阅 [Kubernetes 发行说明和版本偏差 SKU 策略](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)。

### <a id="kubernetes"></a> Kubernetes 群集设置

如果已拥有满足上述必备条件的 Kubernetes 群集，则可以直接跳至[部署步骤](#deploy)。 本节假定你对 Kubernetes 概念有基本的了解。  有关 Kubernetes 的详细信息，请参阅 [Kubernetes 文档](https://kubernetes.io/docs/home)。

可以选择通过以下三种方式中的任意一种部署 Kubernetes：

| 部署 Kubernetes 的位置： | 描述 | 链接 |
|---|---|---|
| **Azure Kubernetes 服务 (AKS)** | Azure 中的托管 Kubernetes 容器服务。 | [说明](deploy-on-aks.md) |
| **多台计算机 (kubeadm)** | 在使用 kubeadm 的物理计算机或虚拟机上部署的 Kubernetes 群集 | [说明](deploy-with-kubeadm.md) |
| **Minikube** | VM 中的单节点 Kubernetes 群集。 | [说明](deploy-on-minikube.md) |

> [!TIP]
> 也可以一步编写 AKS 和大数据群集的部署脚本。 有关详细信息，请参阅如何在 [python 脚本](quickstart-big-data-cluster-deploy.md)或 Azure Data Studio [笔记本](deploy-notebooks.md)中执行此操作。

### <a name="verify-kubernetes-configuration"></a>验证 Kubernetes 配置

运行 kubectl 命令以查看群集配置。 确保 kubectl 指向正确的群集上下文。

```bash
kubectl config view
```

> [!Important] 
> 如果要在使用 kubeadm 引导的多节点 Kuberntes 群集上进行部署，则在启动大数据群集部署之前，请确保在部署所面向的所有 Kubernetes 节点上同步时钟。 大数据群集具有适用于区分时间和时钟偏差的各种服务的内置运行状况属性，可能会导致不正确的状态。

配置 Kubernetes 群集后，可以继续部署新的 SQL Server 大数据群集。 如果要从以前的版本升级，请参阅[如何升级[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](deployment-upgrade.md)。

## <a id="deploy"></a> 部署概述

大多数大数据群集设置都在 JSON 部署配置文件中定义。 在设置期间可以使用 AKS、`kubeadm` 或 `minikube` 的默认部署配置文件，也可以自定义自己的部署配置文件。 出于安全原因，身份验证设置通过环境变量传递。

以下部分详细介绍了如何配置大数据群集部署并提供了常见自定义示例。 此外，你始终可以使用 VS Code 等编辑器编辑自定义部署配置文件。

## <a id="configfile"></a> 默认配置

JSON 配置文件中定义了大数据群集部署选项。 你可以通过用于开发/测试环境的默认设置，开始自定义部署配置文件中的群集部署：

| 部署配置文件 | Kubernetes 环境 |
|---|---|
| **aks-dev-test** | Azure Kubernetes 服务 (AKS) |
| **kubeadm-dev-test** | 多台计算机 (kubeadm) |
| **minikube-dev-test** | minikube |

通过运行 azdata bdc create，即可部署大数据群集。 此操作会提示你选择其中某个默认配置，然后指导你完成部署。

第一次运行 `azdata` 时，必须包含 `--accept-eula=yes` 才能接受最终用户许可协议 (EULA)。

```bash
azdata bdc create --accept-eula=yes
```

在这种情况下，系统会提示你输入不属于默认配置（如密码）的任何设置。 

> [!IMPORTANT]
> 大数据群集的默认名称为 mssql-cluster。 若要运行任何使用 `-n` 参数指定 Kubernetes 命名空间的 kubectl 命令，必须了解这一点。

## <a id="customconfig"></a> 自定义配置

也可以自定义自己的部署配置文件。 可通过以下步骤完成操作：

1. 首先从与 Kubernetes 环境匹配的标准部署配置文件开始。 可以使用 azdata bdc config list 命令列出它们：

   ```bash
   azdata bdc config list
   ```

1. 若要自定义部署，请使用 azdata bdc config init 命令创建部署配置文件的副本。 例如，下面的命令在名为 `custom` 的目标目录中创建 aks-dev-test 部署配置文件的副本：

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   azdata
   > 根据参数指定包含配置文件、 **bdc**和**控件**json 的目录。 `--target` `--source`

1. 若要自定义部署配置文件中的设置，可以在适用于编辑 VS Code 等 JSON 文件的工具中编辑部署配置文件。 对于脚本式自动化，也可以使用 azdata bdc config 命令编辑自定义部署配置文件。 例如，以下命令更改自定义部署配置文件，将部署群集的名称从默认 (mssql-cluster) 更改为 test-cluster：  

   ```bash
   azdata bdc config replace --config-file custom/bdc.json --json-values "metadata.name=test-cluster"
   ```
   
   > [!TIP]
   > 也可以通过在 azdata create bdc 命令中使用 --name 参数，在部署时传入群集名称。 命令中的参数优先于配置文件中的值。

   > 用于查找 JSON 路径的实用工具是 [JSONPath Online Evaluator](https://jsonpath.com/)。

   除了传递键值对之外，还可以提供内联 JSON 值或传递 JSON 补丁文件。 有关详细信息，请参阅[配置大数据群集的部署设置](deployment-custom-configuration.md)。

1. 然后将自定义配置文件传递给 azdata bdc create。 请注意，必须设置所需的[环境变量](#env)，否则系统将提示你输入相应值：

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> 有关部署配置文件结构的详细信息，请参阅[部署配置文件参考](reference-deployment-config.md)。 有关更多配置示例，请参阅[配置大数据群集的部署设置](deployment-custom-configuration.md)。

## <a id="env"></a> 环境变量

以下环境变量用于未存储在部署配置文件中的安全设置。 请注意，可以在配置文件中设置除凭据之外的 Docker 设置。

| 环境变量 | 要求 |描述 |
|---|---|---|
| **CONTROLLER_USERNAME** | Required |群集管理员的用户名。 |
| **CONTROLLER_PASSWORD** | Required |群集管理员的密码。 |
| **MSSQL_SA_PASSWORD** | Required |SQL 主实例的 SA 用户的密码。 |
| **KNOX_PASSWORD** | Required |Knox **root**用户的密码。 请注意，在 "基本身份验证设置" 中，仅支持对 Knox 的用户使用**root**。|
| **ACCEPT_EULA**| 首次使用 `azdata` 时为必需项| 设置为 "是"。 设置为环境变量时，它将 EULA 同时应用于 SQL Server 和 `azdata`。 如果未设置为环境变量，则可以在第一次使用 `azdata` 命令时将 `--accept-eula=yes` 包含在内。|
| **DOCKER_USERNAME** | 可选 | 当容器映像存储在专用存储库中时，用于访问容器映像的用户名。 有关如何使用专用 Docker 存储库部署大数据群集的更多详细信息，请参阅[脱机部署](deploy-offline.md)主题。|
| **DOCKER_PASSWORD** | 可选 |用于访问上述专用存储库的密码。 |

必须先设置这些环境变量，才能调用 azdata bdc create。 如果未设置任何变量，则系统会提示输入变量。

以下示例介绍如何设置适用于 Linux (bash) 和 Windows (PowerShell) 的环境变量：

```bash
export CONTROLLER_USERNAME=admin
export CONTROLLER_PASSWORD=<password>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
export ACCEPT_EULA=yes
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
```

> [!NOTE]
> 必须将**root**用户用于 Knox gateway，其中包含上述密码。 **root**是在此基本身份验证（用户名/密码）安装中支持的唯一用户。 对于 SQL Server master，预配为与上述密码一起使用的用户名是**sa**。


设置环境变量后，必须运行 `azdata bdc create` 才能触发部署。 本示例使用上面创建的群集配置文件：

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

请注意以下原则：

- 如果密码中含有任何特殊字符，请确保使用双引号将密码括起来。 可以将 MSSQL_SA_PASSWORD 设置为自己喜欢的任意形式，但请确保密码足够复杂，且请勿使用 `!`、`&` 或 `'` 字符。 请注意，双引号分隔符仅适用于 bash 命令。
- SA 登录名是安装过程中在 SQL Server 主实例上创建的系统管理员。 创建 SQL Server 容器后，通过在容器中运行 `echo $MSSQL_SA_PASSWORD`，可发现指定的 MSSQL_SA_PASSWORD 环境变量。 出于安全考虑，请根据[此处](../linux/quickstart-install-connect-docker.md#sapassword)所述的最佳做法更改 SA 密码。

## <a id="unattended"></a> 无人参与安装

对于无人参与的部署，必须设置所有所需的环境变量，使用配置文件，并使用 `--accept-eula yes` 参数调用 `azdata bdc create` 命令。 上述部分中的示例介绍了无人参与安装的语法。

## <a id="monitor"></a> 监视部署

在群集启动过程中，客户端命令窗口将输出部署状态。 在部署过程中，应该会看到一系列消息显示它正在等待控制器 Pod：

```output
Waiting for cluster controller to start.
```

15 到 30 分钟后，你应该会收到控制器 Pod 正在运行的消息：

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> 由于下载大数据群集组件的容器映像所需的时间，整个部署可能需要很长时间。 但是，这个过程应不会长达几个小时。 如果你的部署遇到问题，请参阅[监视和故障排除[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](cluster-troubleshooting-commands.md)。

部署完成后，输出会通知你成功：

```output
Cluster deployed successfully.
```

> [!TIP]
> 除非通过自定义配置进行修改，否则部署的大数据群集的默认名称为 `mssql-cluster`。

## <a id="endpoints"></a> 检索终结点

部署脚本成功完成后，可以使用以下步骤获取大数据群集的外部终结点的 IP 地址。

1. 部署完成后，可以从部署标准输出中查找控制器终结点的 IP 地址，也可以通过查看以下 kubectl 命令的 EXTERNAL-IP 输出来查找：

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果在部署过程中没有更改默认名称，请在上一个命令中使用 `-n mssql-cluster`。 mssql-cluster 是大数据群集的默认名称。

1. 使用 [azdata login](reference-azdata.md) 登录大数据群集。 将 --controller-endpoint 参数设置为控制器终结点的外部 IP 地址。

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   指定在部署过程中为控制器配置的用户名和密码（CONTROLLER_USERNAME 和 CONTROLLER_PASSWORD）。

1. 运行 [azdata bdc endpoint list](reference-azdata-bdc-endpoint.md) 以获取一个列表，其中包含每个终结点的描述及其对应的 IP 地址和端口值。 

   ```bash
   azdata bdc endpoint list -o table
   ```

   以下列表显示了此命令的示例输出：

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

也可以通过运行以下 kubectl 命令获取为群集部署的所有服务终结点：

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

### <a name="minikube"></a>Minikube

如果使用的是 minikube，则必须运行以下命令才能获取需要连接的 IP 地址。 除了 IP 外，请指定需要连接的终结点的端口。

```bash
minikube ip
```

## <a id="status"></a> 验证群集状态

部署完成后，可以通过 [azdata bdc status show](reference-azdata-bdc-status.md) 命令检查群集的状态。

```bash
azdata bdc status show
```

> [!TIP]
> 若要运行状态命令，必须先用上述终结点部分中所示的 azdata login 命令登录。

以下显示了此命令的示例输出：

```output
Bdc: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Services: ready                                                                                                                                                                                                     Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Servicename    State    Healthstatus    Details

 sql            ready    healthy         -
 hdfs           ready    healthy         -
 spark          ready    healthy         -
 control        ready    healthy         -
 gateway        ready    healthy         -
 app            ready    healthy         -


 Sql Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Hdfs Services: ready                                                                                                                                                                                                Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 nmnode-0        ready    healthy         StatefulSet nmnode-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
 sparkhead       ready    healthy         StatefulSet sparkhead is healthy


 Spark Services: ready                                                                                                                                                                                               Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Control Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         -
 control         ready    healthy         -
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy


 Gateway Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 gateway         ready    healthy         StatefulSet gateway is healthy


 App Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 appproxy        ready    healthy         ReplicaSet appproxy is healthy
```

还可以通过以下命令获取更详细的状态：

- [azdata bdc 控件状态显示](reference-azdata-bdc-control-status.md)将返回与控制管理服务关联的所有组件的运行状况状态
```
azdata bdc control status show
```
示例输出:
```output
Control: ready                                                                                                                                                                                                      Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         -
 control         ready    healthy         -
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy
```

- **azdata bdc sql 状态显示**将返回 SQL Server 服务的所有资源的运行状况状态
```
azdata bdc sql status show
```
示例输出:
```output
Sql: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
```

> [!IMPORTANT]
> 使用 **--all**参数时，这些命令的输出包含 Kibana 和 Grafana 仪表板的 url，以便进行更详细的分析。

除了使用 azdata 之外，也可以使用 Azure Data Studio 查找终结点和状态信息。 有关通过 azdata 和 Azure Data Studio 查看群集状态的详细信息，请参阅[如何查看大数据群集的状态](view-cluster-status.md)。

## <a id="connect"></a> 连接到群集

有关如何连接到大数据群集的详细信息，请参阅[使用 Azure Data Studio 连接到 SQL Server 大数据群集](connect-to-big-data-cluster.md)。

## <a name="next-steps"></a>后续步骤

若要详细了解大数据群集部署，请参阅下列资源：

- [配置大数据群集的部署设置](deployment-custom-configuration.md)
- [执行 SQL Server 大数据群集的脱机部署](deploy-offline.md)
- [Workshop:Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
