---
title: 如何将 SQL Server 大数据群集在 Kubernetes 上的部署 |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 4db726ac3ceab7649b0a3c04b2c4647b83c7e660
ms.sourcegitcommit: 8aecafdaaee615b4cd0a9889f5721b1c7b13e160
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2018
ms.locfileid: "48818065"
---
# <a name="how-to-deploy-sql-server-big-data-cluster-on-kubernetes"></a>如何将 SQL Server 大数据群集在 Kubernetes 上部署

SQL Server 大数据群集可部署为 docker 容器的 Kubernetes 群集上。 这是安装和配置步骤概述：

- 设置单个 VM，Vm 或 Azure 容器服务中的群集上的 Kubernetes 群集
- 安装群集配置工具`mssqlctl`在客户端计算机上
- 部署 Kubernetes 群集中的 SQL Server 大数据群集

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="kubernetes-prerequisistes"></a>Kubernetes prerequisistes

SQL Server 大数据群集需要的最小 v1.10 版本适用于 Kubernetes、 服务器和客户端。 若要安装 kubectl 客户端上的特定版本，请参阅[安装 kubectl 二进制通过 curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl)。  Minikube 和 AKS 的最新版本是至少 1.10。 适用于 AKS，您将需要使用`--kubernetes-version`参数来指定默认值以外的版本。

此外，请注意，客户端/服务器 Kubernetes 版本，它是倾斜支持为 + /-1 的次要版本。 Kubernetes 文档指出，"客户端应是偏斜的多个次要版本，从主服务器，但可能会导致的最多为 1 个次要版本 master。 例如，v1.3 master 应适用于 v1.1 和 v1.2，v1.3 节点和应使用 v1.2、 v1.3 和 v1.4 客户端。" 有关详细信息，请参阅[Kubernetes 支持的版本和组件倾斜](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)。

## <a id="kubernetes"></a> Kubernetes 群集设置

如果已有的 Kubernetes 群集，满足上述先决条件，则您可以直接跳到[部署步骤](#deploy)。 本部分假定基本了解 Kubernetes 概念。  有关 Kubernetes 的详细信息，请参阅[Kubernetes 文档](https://kubernetes.io/docs/home)。

您可以选择部署在三种方式中的 Kubernetes:

| 部署 Kubernetes 上： | 描述 |
|---|---|
| **Minikube** | 在 VM 中的单节点 Kubernetes 群集。 |
| **Azure Kubernetes 服务 (AKS)** | Azure 中的托管的 Kubernetes 容器服务。 |
| **多个 Vm** | 使用 kubeadm 在 Vm 上部署的 Kubernetes 群集 |

配置其中一个 SQL Server 大数据群集的 Kubernetes 群集选项的指导，请参阅以下文章之一：

   - [配置 Minikube](deploy-on-minikube.md)
   - [Azure Kubernetes 服务上配置 Kubernetes](deploy-on-aks.md)

## <a id="deploy"></a> 部署 SQL Server 大数据群集

配置在 Kubernetes 群集后，你可以继续进行 SQL Server 大数据群集的部署。 若要部署的开发/测试环境的所有默认配置对 Aris 群集，请按照本文中的说明操作：

[快速入门： 部署 Kubernetes 上的 SQL Server Aris](quickstart-big-data-cluster-deploy.md)

如果你想要自定义 Aris 配置，根据工作负荷需求，请按照下一组说明进行操作。

## <a name="verify-kubernetes-configuration"></a>验证 kubernetes 配置

执行以下 kubectl 命令来查看群集配置。 请确保该 kubectl 指向正确的群集上下文。

```bash
kubectl config view
```

## <a name="install-mssqlctl-cli-management-tool-for-sql-server-big-data-cluster"></a>安装 SQL Server 大数据群集 mssqlctl CLI 管理工具
`mssqlctl` 是一个命令行实用工具 Python 编写的可让群集管理员若要启动和管理大数据群集通过 REST Api。 所需的最小的 Python 版本是 3.5 版。 您还必须拥有`pip`用于下载并安装`mssqlctl`工具。 在 Windows 客户端，可以下载必需的 Python 包从[ https://www.python.org/downloads/ ](https://www.python.org/downloads/)。 Python3.5.3 和更高版本，pip3 也会安装时安装 Python。 在安装时可能会不选择添加到路径。 然后您可以找到其中 pip3 位于并手动将其添加到路径。
在 Linux （WSL 或 Ubuntu 客户端示例） 中，这些命令将安装 Python 和 pip 的最新的 3.5 版本：

```bash
sudo apt-get update
sudo apt-get install python3
sudo apt-get install python3-pip
sudo pip3 install --upgrade pip
```

> [!NOTE]
如果您的 Python 安装缺少`requests`包，必须安装`requests`使用`python -m pip install requests`。 如果已有`requests`安装包，请确保通过运行具有最新版本`python -m pip install requests --upgrade`。

运行以下命令来安装 msqlctl:

```bash
pip3 install --index-url https://private-repo.microsoft.com/python/ctp-2.0 mssqlctl
```

## <a name="define-environment-variables"></a>定义环境变量

可以使用一组环境变量传递给自定义群集配置`mssqlctl create cluster`命令。 环境变量的大部分都是可选的默认 avalues 根据下面。 请注意，环境变量，例如需要用户输入的凭据。

| 环境变量 | Required | 默认值 | 描述 |
|---|---|---|---|
| **ACCEPT_EULA** | 用户帐户控制 | N/A | 接受 SQL Server 许可协议 (例如，Y)。  |
| **CLUSTER_NAME** | 用户帐户控制 | N/A | 要部署到 SQLServer 大数据群集的 Kubernetes 命名空间的名称。 |
| **CLUSTER_PLATFORM** | 用户帐户控制 | N/A | 部署 Kubernetes 群集的平台。 可以是`aks`， `minikube`， `kubernetes`|
| **CLUSTER_COMPUTE_POOL_REPLICAS** | 否 | 1 | 计算池副本来构建数。在仅值 CTP2.0 允许为 1。 |
| **CLUSTER_DATA_POOL_REPLICAS** | 否 | 2 | 池中的副本，以生成数据的数目。 |
| **CLUSTER_STORAGE_POOL_REPLICAS** | 否 | 2 | 存储池的副本，以生成数。 |
| **DOCKER_REGISTRY** | 用户帐户控制 | TBD | 用于部署群集的映像的存储位置的专用注册表。 |
| **DOCKER_REPOSITORY** | 用户帐户控制 | TBD | 专用存储库中的上述注册表存储映像。  它是必需的封闭的公共预览版的持续时间。 |
| **DOCKER_USERNAME** | 用户帐户控制 | N/A | 用于访问容器映像，以防在专用存储库中存储的用户名。 它是必需的封闭的公共预览版的持续时间。 |
| **DOCKER_PASSWORD** | 用户帐户控制 | N/A | 用于访问上述的专用存储库的密码。 它是必需的封闭的公共预览版的持续时间。|
| **DOCKER_EMAIL** | 用户帐户控制 | N/A | 与上面的专用存储库关联的电子邮件。 它是必需的封闭的个人预览版的持续时间。 |
| **DOCKER_IMAGE_TAG** | 否 | 最新 | 标签用于标记映像。 |
| **DOCKER_IMAGE_POLICY** | 否 | 始终 | 始终强制的映像拉取。  |
| **DOCKER_PRIVATE_REGISTRY** | 用户帐户控制 | 1 | 为封闭的公共预览版的时间范围内，此值必须设置为 1。 |
| **CONTROLLER_USERNAME** | 用户帐户控制 | N/A | 对于群集管理员用户名。 |
| **CONTROLLER_PASSWORD** | 用户帐户控制 | N/A | 群集管理员的密码。 |
| **KNOX_PASSWORD** | 用户帐户控制 | N/A | Knox 用户的密码。 |
| **MSSQL_SA_PASSWORD** | 用户帐户控制 | N/A | 对于 master 的 SQL 实例 SA 用户 passowrd。 |
| **USE_PERSISTENT_VOLUME** | 否 | true | `true` 若要使用 Kubernetes 永久性卷声明 pod 存储。  `false` 使用临时主机存储为 pod 存储。 请参阅[数据暂留](concept-data-persistence.md)主题的更多详细信息。 |
| **STORAGE_CLASS_NAME** | 否 | 默认值 | 如果`USE_PERSISTENT_VOLUME`是`true`这指示要使用的 Kubernetes 存储类的名称。 请参阅[数据暂留](concept-data-persistence.md)主题的更多详细信息。 |
| **MASTER_SQL_PORT** | 否 | 31433 | 主 SQL 实例在公用网络进行侦听 TCP/IP 端口。 |
| **KNOX_PORT** | 否 | 30443 | Apache Knox 在公用网络进行侦听 TCP/IP 端口。 |
| **GRAFANA_PORT** | 否 | 30888 | 监视应用程序 Grafana 在公用网络进行侦听 TCP/IP 端口。 |
| **KIBANA_PORT** | 否 | 30999 | Kibana 日志搜索应用程序在公用网络进行侦听 TCP/IP 端口。 |



> [!IMPORTANT]
>1. 受限个人预览版期间，专用 Docker 注册表的凭据将向您提供在会审您[EAP 注册](https://aka.ms/eapsignup)。
>1. 在本地群集使用 kubeadm，环境变量的值构建`CLUSTER_PLATFORM`是`kubernetes`。 此外，当 USE_PERSISTENT_STORAGE = true，必须预先预配 Kubernetes 存储类并将其传递通过使用 STORAGE_CLASS_NAME。
>1. 请确保你在双引号内包装密码，如果它包含任何特殊字符。 您可以设置 MSSQL_SA_PASSWORD 为您希望的任何内容，但请确保它们是足够复杂并且不使用`!`，`&`或`‘`字符。 请注意，双引号分隔符仅适用于 bash 命令。
>1. 群集的名称必须仅小写字母数字字符，不留空格。 将在具有与群集相同的名称的命名空间中创建群集的所有 Kubernetes 项目 （容器、 pod、 有状态集、 服务） 指定的名称。
>1. **SA**帐户是在安装过程中创建的 SQL Server 主实例上的系统管理员。 创建 SQL Server 容器，你指定的 MSSQL_SA_PASSWORD 环境变量是可发现通过运行后回显 $MSSQL_SA_PASSWORD 容器中。 出于安全考虑，更改 SA 密码根据最佳实践[此处](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password)。

设置环境变量所需的部署 Aris 根据使用的 Windows 或 Linux 客户端不同的群集。  选择以下步骤使用具体取决于哪个操作系统。

初始化以下环境变量，它们所需的部署群集：

### <a name="windows"></a>Windows

使用 CMD 窗口 (而不是 PowerShell)，配置以下环境变量：

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=<minikube or aks or kubernetes>

SET CONTROLLER_USERNAME=<controller_admin_name – can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instances>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username>
SET DOCKER_PASSWORD=<your password>
SET DOCKER_EMAIL=<your Docker email, use same as username provided>
SET DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="linux"></a>Linux

初始化以下环境变量：

```bash
export ACCEPT_EULA=Y
export CLUSTER_PLATFORM=<minikube or aks or kubernetes>

export CONTROLLER_USERNAME=<controller_admin_name – can be anything>
export CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
export KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
export MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instances>

export DOCKER_REGISTRY=private-repo.microsoft.com
export DOCKER_REPOSITORY=mssql-private-preview
export DOCKER_USERNAME=<your username>
export DOCKER_PASSWORD=<your password>
export DOCKER_EMAIL=<your Docker email, use same as username provided>
export DOCKER_PRIVATE_REGISTRY="1"
```

## <a name="deploy-sql-server-big-data-cluster"></a>部署 SQL Server 大数据群集

创建群集 API 用于初始化 Kubernetes 命名空间并将其部署到该命名空间的所有应用程序 pod。 若要部署 Kubernetes 群集上的 SQL Server 大数据群集，请运行以下命令：

```bash
mssqlctl create cluster <name of your cluster>
```

在群集启动客户端命令窗口中的部署状态将输出。 此外可以通过不同的命令窗口中运行以下命令检查部署状态：

```bash
kubectl get all -n <name of your cluster>
kubectl get pods -n <name of your cluster>
kubectl get svc -n <name of your cluster>
```

运行，可以查看更精细的状态和配置每个 pod:
```bash
kubectl describe pod <pod name> -n <name of your cluster>
```

控制器 pod 运行后，您可以利用群集管理门户来监视部署中的部署选项卡。

## <a id="masterip"></a> 获取 SQL Server 主实例和 SQL Server 大数据群集 IP 地址

部署脚本已成功完成后，可以获取如下所述的步骤的 SQL Server 主实例的 IP 地址。 将使用此 IP 地址和端口号 31433 连接到 SQL Server 主实例 (例如：  **\<ip 地址\>、 31433**)。 同样，对于 SQL Server 大数据群集 IP。 群集管理门户中的服务终结点选项卡中概述了群集的所有终结点。 可以使用群集管理门户来监视部署。 您可以访问在门户中使用的外部 IP 地址和端口号`service-proxy-lb`(例如： **https://\<ip 地址\>: 30777**)。 凭据的访问管理门户中的值`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`上面提供的环境变量。

### <a name="aks"></a>AKS

如果使用 AKS，Azure 提供了 Azure 负载均衡器服务。 运行以下命令：

```bash
kubectl get svc service-master-pool-lb -n <name of your cluster>
kubectl get svc service-security-lb -n <name of your cluster>
kubectl get svc service-proxy-lb -n <name of your cluster>
```

寻找**外部 IP**分配给服务的值。 然后，连接到 SQL Server 主实例端口 31433 在使用的 IP 地址 (例如：  **\<ip 地址\>、 31433**) 和 SQL Server 大数据群集终结点使用的外部 IP`service-security-lb`服务。 

### <a name="minikube"></a>Minikube

如果使用 Minikube，您需要运行以下命令来获取 IP 地址连接到所需。 除了 IP，指定您需要连接到终结点的端口。 若要获取的所有服务终结点 

```bash
minikube ip
```

不管平台如何在 Kubernetes 群集上运行，若要获取针对的群集，运行以下命令部署的所有服务终结点：
```bash
kubectl get svc -n <name of your cluster>
```

## <a name="next-steps"></a>后续步骤

已成功部署 SQL Server 大数据后到 Kubernetes 群集[安装的大数据工具](deploy-big-data-tools.md)并尝试一些新功能并了解[如何在 SQL Server 2019 预览版中使用笔记本](notebooks-guidance.md)。
