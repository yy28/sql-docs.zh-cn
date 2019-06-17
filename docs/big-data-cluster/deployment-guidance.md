---
title: 部署指南
titleSuffix: SQL Server big data clusters
description: 了解如何将部署在 Kubernetes 上的 SQL Server 2019 大数据群集 （预览版）。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 15cd412de1dda9d1245859c27d35a7c7f9f52710
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782247"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>如何部署 SQL Server 大数据群集在 Kubernetes 上

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 大数据群集部署为 docker 容器的 Kubernetes 群集上。 这是安装和配置步骤概述：

- 设置一个单独的 VM 的 Vm，或在 Azure Kubernetes 服务 (AKS) 群集上的 Kubernetes 群集。
- 安装群集配置工具**mssqlctl**在客户端计算机上。
- 部署 Kubernetes 群集中的 SQL Server 大数据群集。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>安装 SQL Server 2019 大数据工具

首次部署 SQL Server 2019 大数据群集之前[安装的大数据工具](deploy-big-data-tools.md):

- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 扩展**

## <a id="prereqs"></a> Kubernetes 先决条件

SQL Server 大数据群集至少需要版本最低为 Kubernetes 的 v1.10 服务器和客户端 (kubectl)。

> [!NOTE]
> 请注意，客户端和服务器的 Kubernetes 版本应为 + 1 或-1 的次要版本中。 有关详细信息，请参阅[Kubernetes 支持的版本和组件倾斜](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)。

### <a id="kubernetes"></a> Kubernetes 群集设置

如果您已有满足上述先决条件的 Kubernetes 群集，则可以直接跳到[部署步骤](#deploy)。 本部分假定基本了解 Kubernetes 概念。  有关 Kubernetes 的详细信息，请参阅[Kubernetes 文档](https://kubernetes.io/docs/home)。

您可以选择部署在三种方式中的 Kubernetes:

| 部署 Kubernetes 上： | Description | 链接 |
|---|---|---|
| **Azure Kubernetes 服务 (AKS)** | Azure 中的托管的 Kubernetes 容器服务。 | [说明](deploy-on-aks.md) |
| **多台计算机 (kubeadm)** | 物理计算机或使用虚拟机上部署的 Kubernetes 群集**kubeadm** | [说明](deploy-with-kubeadm.md) |
| **Minikube** | 在 VM 中的单节点 Kubernetes 群集。 | [说明](deploy-on-minikube.md) |

> [!TIP]
> 部署 AKS 和大数据群集在一个步骤中 SQL Server 的示例 python 脚本，请参阅[快速入门：部署大数据群集在 Azure Kubernetes 服务 (AKS) 的 SQL Server](quickstart-big-data-cluster-deploy.md)。

### <a name="verify-kubernetes-configuration"></a>验证 Kubernetes 配置

运行**kubectl**命令以查看群集配置。 请确保该 kubectl 指向正确的群集上下文。

```bash
kubectl config view
```

配置在 Kubernetes 群集后，可以继续进行新的 SQL Server 大数据群集的部署。 如果要从以前的版本进行升级，请参阅[如何升级 SQL Server 大数据群集](deployment-upgrade.md)。

## <a id="deploy"></a> 部署概述

从 ctp 版本 2.5 开始，JSON 部署配置文件中定义大多数大数据群集设置。 可以使用 AKS，kubeadm，默认的部署配置文件或 minikube 或您可以自定义你自己的部署配置文件，若要在安装期间使用。 出于安全原因，通过环境变量传递身份验证设置。

以下部分提供有关如何配置你的大数据的更多详细信息群集部署，以及常见的自定义的示例。 此外，您始终可以编辑自定义部署配置文件，例如使用 VSCode 等编辑器。

## <a id="configfile"></a> 默认配置

大数据群集的部署选项在 JSON 配置文件中定义。 有三个标准部署配置文件使用默认设置开发/测试环境：

| 部署配置文件 | Kubernetes 环境 |
|---|---|
| **aks-dev-test.json** | Azure Kubernetes 服务 (AKS) |
| **kubeadm-dev-test.json** | 多台计算机 (kubeadm) |
| **minikube-dev-test.json** | Minikube |

可以通过运行部署大数据群集**mssqlctl 群集创建**。 这会提示您选择一种默认配置，并会引导你完成部署。

```bash
mssqlctl cluster create
```

在此方案中，系统会提示输入不是默认配置，如密码的一部分的任何设置。 请注意，Docker 信息向你由 Microsoft 提供的 SQL Server 2019 一部分[早期采用计划](https://aka.ms/eapsignup)。

> [!IMPORTANT]
> 大数据群集的默认名称是**mssql 群集**。 务必知道，才能运行任何这一点**kubectl**指定与 Kubernetes 命名空间的命令`-n`参数。

## <a id="customconfig"></a> 自定义配置

还有可能要自定义部署配置文件。 可以使用以下步骤来执行此操作：

1. 开始使用 Kubernetes 环境匹配的标准部署配置文件之一。 可以使用**mssqlctl 群集配置列表**命令以列出它们：

   ```bash
   mssqlctl cluster config list
   ```

1. 若要自定义你的部署，请创建的部署配置文件的一份**mssqlctl 群集配置 init**命令。 例如，以下命令将创建一份**aks 开发 test.json**当前目录中的部署配置文件：

   ```bash
   mssqlctl cluster config init --src aks-dev-test.json --target custom.json
   ```

1. 若要自定义部署配置文件中的设置，可以在一种工具，适用于编辑 json 文档，如 VS Code 中编辑它。 对于脚本化自动化，你可以编辑自定义配置文件使用**mssqlctl 群集配置部分，设置**命令。 例如，以下命令可更改要更改已部署群集的名称从默认的自定义配置文件 (**mssql 群集**) 到**测试群集**:  

   ```bash
   mssqlctl cluster config section set --config-file custom.json --json-values "metadata.name=test-cluster"
   ```

   > [!TIP]
   > 是用于查找 JSON 路径的有用工具[JSONPath 联机计算器](https://jsonpath.com/)。

   除了传递键 / 值对，还可以提供 JSON 值的内联或传递 JSON 修补程序文件。 有关详细信息，请参阅[配置的大数据群集部署设置](deployment-custom-configuration.md)。

1. 然后，将传递到自定义配置文件**mssqlctl 群集创建**。 请注意，必须设置所需[环境变量](#env)，否则系统将提示输入值：

   ```bash
   mssqlctl cluster create --config-file custom.json --accept-eula yes
   ```

> [!TIP]
> 部署配置文件的结构的详细信息，请参阅[部署配置文件引用](reference-deployment-config.md)。 有关更多的配置示例，请参阅[配置的大数据群集部署设置](deployment-custom-configuration.md)。

## <a id="env"></a> 环境变量

以下环境变量用于未存储在一个部署配置文件的安全设置。 请注意，可以在配置文件中设置 Docker 设置凭据除外。

| 环境变量 | Description |
|---|---|---|---|
| **DOCKER_USERNAME** | 用于访问容器映像，以防在专用存储库中存储的用户名。 |
| **DOCKER_PASSWORD** | 用于访问上述的专用存储库的密码。 |
| **CONTROLLER_USERNAME** | 对于群集管理员用户名。 |
| **CONTROLLER_PASSWORD** | 群集管理员的密码。 |
| **KNOX_PASSWORD** | Knox 用户的密码。 |
| **MSSQL_SA_PASSWORD** | 对于 master 的 SQL 实例 SA 用户的密码。 |

在调用之前，必须设置这些环境变量**mssqlctl 群集创建**。 如果未设置任何变量，则会提示输入它。

下面的示例演示如何设置适用于 Linux (bash) 和 Windows (PowerShell) 的环境变量：

```bash
export CONTROLLER_USERNAME=admin
export CONTROLLER_PASSWORD=<password>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
export DOCKER_USERNAME=<docker-username>
export DOCKER_PASSWORD=<docker-password>
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
SET DOCKER_USERNAME=<docker-username>
SET DOCKER_PASSWORD=<docker-password>
```

在设置环境变量，您必须运行`mssqlctl cluster create`就能触发部署。 此示例使用上面创建的群集配置文件：

```
mssqlctl cluster create --config-file custom.json --accept-eula yes
```

请注意以下准则：

- 在此期间，专用 Docker 注册表的凭据将向您提供在会审您[早期采用计划注册](https://aka.ms/eapsignup)。 测试 SQL Server 大数据群集所需早期采用计划注册。
- 请确保你在双引号内包装密码，如果它包含任何特殊字符。 可以设置**MSSQL_SA_PASSWORD**任何您喜欢，但请确保密码不够复杂和不使用`!`，`&`或`'`字符。 请注意，双引号分隔符仅适用于 bash 命令。
- **SA**登录名是在安装过程中创建的 SQL Server 主实例上的系统管理员。 创建 SQL Server 容器后, **MSSQL_SA_PASSWORD**您指定的环境变量是可发现通过运行回显 $MSSQL_SA_PASSWORD 容器中的。 出于安全考虑，更改 SA 密码根据最佳实践[此处](../linux/quickstart-install-connect-docker.md#sapassword)。

## <a id="unattended"></a> 无人参与的安装

有关无人参与部署，必须设置所有必需的环境变量，使用配置文件，并调用`mssqlctl cluster create`命令与`--accept-eula yes`参数。 上一节中的示例演示用于无人参与安装的语法。

## <a id="monitor"></a> 监视部署

在群集启动期间客户端命令窗口将输出的部署状态。 在部署过程中，您应看到一系列消息，它正在等待控制器 pod:

```output
2019-04-12 14:40:10.0129 UTC | INFO | Waiting for controller pod to be up...
```

小于 15 到 30 分钟后，您应会收到通知，正在运行的控制器 pod:

```output
2019-04-12 15:01:10.0809 UTC | INFO | Waiting for controller pod to be up. Checkthe mssqlctl.log file for more details.
2019-04-12 15:01:40.0861 UTC | INFO | Controller pod is running.
2019-04-12 15:01:40.0884 UTC | INFO | Controller Endpoint: https://<ip-address>:30080
```

> [!IMPORTANT]
> 整个部署可能需要很长时间由于下载的大数据群集组件的容器映像所需的时间。 但是，也不会花费几个小时。 如果遇到你的部署的问题，请参阅[监视和故障排除 SQL Server 大数据群集](cluster-troubleshooting-commands.md)。

部署完成后，输出会通知您成功：

```output
2019-04-12 15:37:18.0271 UTC | INFO | Monitor and track your cluster at the Portal Endpoint: https://<ip-address>:30777/portal/
2019-04-12 15:37:18.0271 UTC | INFO | Cluster deployed successfully.
```

记下的 URL**门户终结点**以便在下一节中使用前面的输出中。

> [!TIP]
> 已部署的大数据群集的默认名称是`mssql-cluster`除非自定义配置已更改。

## <a id="endpoints"></a> 检索终结点

部署脚本已成功完成时，可以获得使用以下步骤在大数据群集的外部终结点的 IP 地址。

1. 部署后，通过查看以下的外部 IP 输出查找控制器终结点的 IP 地址**kubectl**命令：

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果在部署期间未更改默认名称，使用`-n mssql-cluster`在前一命令中。 **mssql 群集**是大数据群集的默认名称。

1. 登录到大数据群集**mssqlctl 登录**。 设置 **-控制器终结点**控制器终结点的外部 IP 地址的参数。

   ```bash
   mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   在部署过程中指定的用户名和密码配置为控制器 （CONTROLLER_USERNAME 和 CONTROLLER_PASSWORD）。

1. 运行**mssqlctl 群集终结点列表**以获取每个终结点和其对应的 IP 地址和端口值的说明的列表。 

   ```bash
   mssqlctl cluster endpoint list
   ```

   以下列表显示了此命令的示例输出：

   ```output
   Name               Description                                             Endpoint                                                   Ip              Port    Protocol
   -----------------  ------------------------------------------------------  ---------------------------------------------------------  --------------  ------  ----------
   gateway            Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  30443   https
   spark-history      Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  30443   https
   yarn-ui            Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  30443   https
   app-proxy          Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  30778   https
   management-proxy   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  30777   https
   portal             Management Portal                                       https://11.111.111.111:30777/portal                        11.111.111.111  30777   https
   log-search-ui      Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  30777   https
   metrics-ui         Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  30777   https
   controller         Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  30080   https
   sql-server-master  SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  31433   tcp
   webhdfs            HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  30443   https
   livy               Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  30443   https
   ```

### <a name="minikube"></a>Minikube

如果使用 minikube，您需要运行以下命令来获取 IP 地址连接到所需。 除了 IP，指定您需要连接到终结点的端口。

```bash
minikube ip
```

不管平台如何在 Kubernetes 群集上运行，若要获取针对的群集，运行以下命令部署的所有服务终结点：

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

## <a id="connect"></a> 连接到群集

有关如何连接到大数据群集的详细信息，请参阅[连接到 SQL Server 大数据群集使用 Azure Data Studio](connect-to-big-data-cluster.md)。

## <a name="next-steps"></a>后续步骤

若要了解有关大数据群集部署的详细信息，请参阅以下资源：

- [配置大数据群集的部署设置](deployment-custom-configuration.md)
- [执行 SQL Server 大数据群集的脱机部署](deploy-offline.md)
- [研讨会：Microsoft SQL Server 大数据群集体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
