---
title: 部署 SQL Server 大数据群集 |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: quickstart
ms.prod: sql
ms.openlocfilehash: 5781b3acfd2262b3a3be540abb331839dfcc56c6
ms.sourcegitcommit: 08b3de02475314c07a82a88c77926d226098e23f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2018
ms.locfileid: "49120454"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>快速入门： 部署 SQL Server 大数据群集在 Azure Kubernetes 服务 (AKS)

在此快速入门中，您将在默认配置适用于开发/测试环境中在 AKS 上中安装 SQL Server 大数据群集。 除了 SQL 主实例，群集将包括一个计算池实例、 一个数据池实例和两个存储池实例。 使用 AKS 默认存储类之上预配 Kubernetes 永久性卷将保留数据。 在中[部署指南](deployment-guidance.md)主题可以找到一组可用于进一步自定义配置的环境变量。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>必要條件

本快速入门教程要求您已具有的最低版本为 v1.10 中配置了 AKS 群集。 有关详细信息，请参阅[部署在 AKS 上](deploy-on-aks.md)指南。

在您用来运行命令以安装 SQL Server 大数据群集的计算机，你需要安装[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)。 SQL Server 大数据群集需要版本最低为 1.10 适用于 Kubernetes、 服务器和客户端 (kubectl)。 若要安装 kubectl，请参阅[安装 kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl)。 

若要安装`mssqlctl`CLI 工具，用于管理 SQL Server 大数据群集在客户端计算机上，您必须首先安装[Python](https://www.python.org/downloads/)最低版本 3.0 版和[pip3](https://pip.pypa.io/en/stable/installing/)。 请注意是否使用至少 3.4 从下载的 Python 版本已安装 pip [python.org](https://www.python.org/)。

如果您的 Python 安装缺少`requests`包，必须安装`requests`使用`python -m pip install requests`。 如果已有`requests`包将其升级到最新版本使用`python -m pip install requests --upgrade`。

## <a name="verify-aks-configuration"></a>验证 AKS 配置

部署 AKS 群集后，可以执行以下 kubectl 命令来查看群集配置。 请确保该 kubectl 指向正确的群集上下文。

```bash
kubectl config view
```

## <a name="install-mssqlctl-cli-management-tool"></a>安装 mssqlctl CLI 管理工具

运行以下命令以安装`mssqlctl`在客户端计算机上的工具。 相同命令从 Windows 和 Linux 客户端的工作原理，但请确保在 Windows 使用管理特权运行在 cmd 窗口中运行它或前缀与`sudo`Linux 上：

```
pip3 install --index-url https://private-repo.microsoft.com/python/ctp-2.0 mssqlctl  
```

## <a name="define-environment-variables"></a>定义环境变量

根据使用的 Windows 或 Linux/macOS 客户端设置环境变量所需的部署大数据群集略有不同。  选择以下步骤使用具体取决于哪个操作系统。

在继续之前，请注意以下重要准则：

- 请确保你在双引号内包装密码，如果它包含任何特殊字符。 请注意，双引号分隔符仅适用于 bash 命令。
- 您可以将密码设置环境变量为您希望的任何内容，但请确保它们是足够复杂并且不使用`!`， `&`，或`‘`字符。
- 对于 CTP 2.0 版本中，不要更改默认端口。
- **SA**帐户是在安装过程中创建的 SQL Server 主实例上的系统管理员。 创建 SQL Server 容器，你指定的 MSSQL_SA_PASSWORD 环境变量是可发现通过运行后回显 $MSSQL_SA_PASSWORD 容器中。 出于安全考虑，更改 SA 密码根据最佳实践[此处](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password)。

初始化以下环境变量。  它们所需的部署大数据群集：

### <a name="windows"></a>Windows

使用 CMD 窗口 (而不是 PowerShell)，配置以下环境变量：

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=aks

SET CONTROLLER_USERNAME=<controller_admin_name – can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username, credentials provided by Microsoft>
SET DOCKER_PASSWORD=<your password, credentials provided by Microsoft>
SET DOCKER_EMAIL=<your Docker email, use the username provided by Microsoft>
SET DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="linuxmacos"></a>Linux/macOS

初始化以下环境变量：

```bash
export ACCEPT_EULA=Y
export CLUSTER_PLATFORM=aks

export CONTROLLER_USERNAME=<controller_admin_name – can be anything>
export CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
export KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
export MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

export DOCKER_REGISTRY=private-repo.microsoft.com
export DOCKER_REPOSITORY=mssql-private-preview
export DOCKER_USERNAME=<your username, credentials provided by Microsoft>
export DOCKER_PASSWORD=<your password, credentials provided by Microsoft>
export DOCKER_EMAIL=<your Docker email, use the username provided by Microsoft>
export DOCKER_PRIVATE_REGISTRY="1"
```

> [!NOTE]
> 在有限的公共预览期，若要下载 SQL Server 大数据群集映像的 Docker 凭据由 Microsoft 提供向每个客户。 若要请求访问权限，注册[此处](https://aka.ms/eapsignup)，并指定你感兴趣，若要试用 SQL Server 大数据群集。

## <a name="deploy-a-big-data-cluster"></a>部署大数据群集

若要部署 Kubernetes 群集上的 SQL Server 2019 CTP 2.0 大数据群集，运行以下命令：

```bash
mssqlctl create cluster <name of your cluster>
```

> [!NOTE]
> 群集的名称必须是仅小写字母数字字符，不留空格。 将在具有与群集相同的名称的命名空间中创建的大数据群集的所有 Kubernetes 项目指定名称。


在命令窗口将输出的部署状态。 此外可以通过不同的命令窗口中运行以下命令检查部署状态：

```bash
kubectl get all -n <name of your cluster>
kubectl get pods -n <name of your cluster>
kubectl get svc -n <name of your cluster>
```

运行，可以查看更精细的状态和配置每个 pod:
```bash
kubectl describe pod <pod name> -n <name of your cluster>
```

控制器 pod 运行后，可以使用群集管理门户来监视部署。 您可以访问在门户中使用的外部 IP 地址和端口号`service-proxy-lb`(例如： **https://\<ip 地址\>: 30777**)。 凭据的访问管理门户中的值`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`上面提供的环境变量。

可以通过在 bash 或 cmd 窗口中运行此命令获取服务代理 lb 服务的 IP 地址：

```bash
kubectl get svc service-proxy-lb -n <name of your cluster>
```

> [!NOTE]
> 访问 web 页，因为我们要使用自动生成的 SSL 证书时，您将看到一条安全警告。 在将来的版本中，我们将提供的功能来提供自己的签名的证书。
 

## <a name="connect-to-the-big-data-cluster"></a>连接到大数据群集

部署脚本已成功完成后，可以获取 IP 地址的 SQL Server 主实例和 Spark/HDFS 终结点使用如下所述的步骤。 所有群集终结点将都显示在也以方便引用群集管理门户中的服务终结点部分。

Azure 提供了到 AKS 的 Azure 负载均衡器服务。 运行以下命令在 cmd 或 bash 窗口：

```bash
kubectl get svc service-master-pool-lb -n <name of your cluster>
kubectl get svc service-security-lb -n <name of your cluster>
```

寻找**外部 IP**分配给服务的值。 连接到 SQL Server 主实例使用的 IP 地址`service-master-pool-lb`在端口 31433 (Ex:  **\<ip 地址\>、 31433**) 和 SQL Server 大数据群集终结点使用的外部 IP`service-security-lb`服务。   大数据群集终结点是可在此与 HDFS 进行交互，并提交 Spark 作业通过 Knox。

## <a name="next-steps"></a>后续步骤

现在，已部署 SQL Server 大数据群集，请尝试一些新功能：

> [!div class="nextstepaction"]
> [如何在 SQL Server 2019 预览版中使用笔记本](notebooks-guidance.md)
