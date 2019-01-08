---
title: 部署快速入门
titleSuffix: SQL Server 2019 big data clusters
description: 演练的 SQL Server 2019 大数据群集 （预览版） 在 Azure Kubernetes 服务 (AKS) 的部署。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: quickstart
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: f5ddd80eaf29db657c42eec5c84c8485e8b0d8b6
ms.sourcegitcommit: 85fd3e1751de97a16399575397ab72ebd977c8e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/17/2018
ms.locfileid: "53531152"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>快速入门：部署 SQL Server 大数据群集在 Azure Kubernetes 服务 (AKS)

在此快速入门中，你将在默认配置适用于开发/测试环境中在 AKS 上中部署 SQL Server 2019 大数据群集 （预览版）。

> [!NOTE]
> AKS 是只需一个位置移动到主机 Kubernetes。 大数据群集可以部署到 Kubernetes 中，而不考虑基础结构。 有关详细信息，请参阅[如何部署 SQL Server 大数据群集在 Kubernetes 上](deployment-guidance.md)。

除了 SQL 主实例中，群集包含一个计算池实例、 一个数据池实例和两个存储池实例。 数据将保留使用使用 AKS 默认存储类的 Kubernetes 永久性卷。 若要进一步自定义你的配置，请参阅中的环境变量[部署指南](deployment-guidance.md)。

如果你想要运行脚本，以创建 AKS 群集和在同一时间安装的大数据群集，请参阅[部署大数据群集在 Azure Kubernetes 服务 (AKS) SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks)。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>先决条件

本快速入门教程要求您已具有的最低版本为 v1.10 中配置了 AKS 群集。 有关详细信息，请参阅[部署在 AKS 上](deploy-on-aks.md)指南。

- [SQL Server 2019 大数据工具](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
   - **Kubectl**
   - **mssqlctl**

## <a name="verify-aks-configuration"></a>验证 AKS 配置

部署 AKS 群集后，可以执行以下 kubectl 命令来查看群集配置。 请确保该 kubectl 指向正确的群集上下文。

```bash
kubectl config view
```

## <a name="define-environment-variables"></a>定义环境变量

根据使用的 Windows 或 Linux/macOS 客户端设置环境变量所需的部署大数据群集略有不同。  选择以下步骤使用具体取决于哪个操作系统。

在继续之前，请注意以下重要准则：

- 在中[命令窗口](https://docs.microsoft.com/visualstudio/ide/reference/command-window)，引号包含环境变量中。 如果使用引号来包装一个密码，密码中包含引号。
- 在 bash 中，该变量中不包括引号。 我们的示例使用双引号`"`。
- 您可以将密码设置环境变量为您希望的任何内容，但请确保它们是足够复杂并且不使用`!`， `&`，或`'`字符。
- `sa`帐户是在安装过程中创建的 SQL Server 主实例上的系统管理员。 创建 SQL Server 容器后，通过在容器中运行 `echo $MSSQL_SA_PASSWORD`，可发现指定的 `MSSQL_SA_PASSWORD` 环境变量。 出于安全考虑，更改你`sa`密码根据最佳实践[此处](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password)。

初始化以下环境变量。  它们所需的部署大数据群集：

### <a name="windows"></a>Windows

使用命令窗口 (而不是 PowerShell)，配置以下环境变量：

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=aks

SET CONTROLLER_USERNAME=<controller_admin_name - can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password - can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password - can be anything, password complexity compliant>
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
export ACCEPT_EULA="Y"
export CLUSTER_PLATFORM="aks"

export CONTROLLER_USERNAME="<controller_admin_name - can be anything>"
export CONTROLLER_PASSWORD="<controller_admin_password - can be anything, password complexity compliant>"
export KNOX_PASSWORD="<knox_password - can be anything, password complexity compliant>"
export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

export DOCKER_REGISTRY="private-repo.microsoft.com"
export DOCKER_REPOSITORY="mssql-private-preview"
export DOCKER_USERNAME="<your username, credentials provided by Microsoft>"
export DOCKER_PASSWORD="<your password, credentials provided by Microsoft>"
export DOCKER_EMAIL="<your Docker email, use the username provided by Microsoft>"
export DOCKER_PRIVATE_REGISTRY="1"
```

> [!NOTE]
> 在有限的公共预览期，若要下载 SQL Server 大数据群集映像的 Docker 凭据由 Microsoft 提供向每个客户。 若要请求访问权限，注册[此处](https://aka.ms/eapsignup)，并指定你感兴趣，若要试用 SQL Server 大数据群集。

## <a name="deploy-a-big-data-cluster"></a>部署大数据群集

若要部署 Kubernetes 群集上的 SQL Server 2019 CTP 2.2 大数据群集，运行以下命令：

```bash
mssqlctl create cluster <your-cluster-name>
```

> [!NOTE]
> 群集的名称必须是仅小写字母数字字符，不留空格。 将在具有与群集相同的名称的命名空间中创建的大数据群集的所有 Kubernetes 项目指定名称。

命令窗口或命令行程序返回的部署状态。 此外可以通过不同的命令窗口中运行以下命令检查部署状态：

```bash
kubectl get all -n <your-cluster-name>
kubectl get pods -n <your-cluster-name>
kubectl get svc -n <your-cluster-name>
```

运行，可以查看更精细的状态和配置每个 pod:
```bash
kubectl describe pod <pod name> -n <your-cluster-name>
```

> [!TIP]
> 有关如何监视和排查部署问题的更多详细信息，请参阅[部署故障排除](deployment-guidance.md#troubleshoot)一部分部署的指导文章。

## <a name="open-the-cluster-administration-portal"></a>打开群集管理门户

控制器 pod 运行后，可以使用群集管理门户来监视部署。 您可以访问在门户中使用的外部 IP 地址和端口号`service-proxy-lb`(例如： **https://\<ip 地址\>: 30777/门户**)。 凭据的访问管理门户中的值`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`上面提供的环境变量。

可以通过在 bash 或 cmd 窗口中运行此命令获取服务代理 lb 服务的 IP 地址：

```bash
kubectl get svc service-proxy-lb -n <your-cluster-name>
```

> [!NOTE]
> 访问 web 页，因为我们要使用自动生成的 SSL 证书时，您将看到一条安全警告。 在将来的版本中，我们将提供的功能来提供自己的签名的证书。

## <a name="connect-to-the-big-data-cluster"></a>连接到大数据群集

部署脚本已成功完成后，可以获取 IP 地址的 SQL Server 主实例和 Spark/HDFS 终结点使用如下所述的步骤。 所有群集终结点将都显示在也以方便引用群集管理门户中的服务终结点部分。

Azure 提供了到 AKS 的 Azure 负载均衡器服务。 运行以下命令在 cmd 或 bash 窗口：

```bash
kubectl get svc endpoint-master-pool -n <your-cluster-name>
kubectl get svc service-security-lb -n <your-cluster-name>
```

寻找**外部 IP**分配给服务的值。 连接到 SQL Server 主实例使用的 IP 地址`endpoint-master-pool`在端口 31433 (Ex:  **\<ip 地址\>、 31433**) 和 SQL Server 大数据群集终结点使用的外部 IP`service-security-lb`服务。   大数据群集终结点是可在此与 HDFS 进行交互，并提交 Spark 作业通过 Knox。

## <a name="next-steps"></a>后续步骤

现在，已部署 SQL Server 大数据群集，请尝试一些新功能：

> [!div class="nextstepaction"]
> [如何在 SQL Server 2019 预览版中使用笔记本](notebooks-guidance.md)
