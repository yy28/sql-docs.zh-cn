---
title: 使用 azdate 部署应用程序
titleSuffix: SQL Server big data clusters
description: 在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 上将 Python 或 R 脚本部署为应用程序。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 863b569014bf35ef4e6aab01ba966edb34812bd1
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532515"
---
# <a name="how-to-deploy-an-app-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>如何在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 上部署应用

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何将 R 和 Python 脚本作为应用程序在 SQL Server 2019 大数据群集中进行部署和管理。

## <a name="whats-new-and-improved"></a>新增和改进的内容

- 用于管理群集和应用程序的单个命令行实用程序。
- 简化应用程序部署，同时通过规范文件提供精细控制。
- 支持托管其他应用程序类型 - SSIS 和 MLeap（CTP 2.3 中的新增功能）。
- 用于管理应用程序部署的 [Visual Studio Code 扩展](app-deployment-extension.md)。

使用 `azdata` 命令行实用程序部署和管理应用程序。 本文提供了有关如何从命令行部署应用的示例。 要了解如何在 Visual Studio Code 中使用它，请参阅 [Visual Studio Code 扩展](app-deployment-extension.md)。

支持下列应用类型：
- R 和 Python 应用（函数、模型和应用）
- MLeap 服务
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>必备条件

- [SQL Server 2019 大数据群集](deployment-guidance.md)
- [azdata 命令行工具](deploy-install-azdata.md)

## <a name="capabilities"></a>功能

在 SQL Server 2019（预览版）中，可以创建、删除、描述、初始化、列出运行和更新应用程序。 下表介绍了可以与 azdata 一起使用的应用程序部署命令  。

|Command |描述 |
|:---|:---|
|`azdata login` | 登录到 SQL Server 大数据群集 |
|`azdata app create` | 创建应用程序。 |
|`azdata app delete` | 删除应用程序。 |
|`azdata app describe` | 描述应用程序。 |
|`azdata app init` | Kickstart 新应用程序主干。 |
|`azdata app list` | 列出应用程序。 |
|`azdata app run` | 运行应用程序。 |
|`azdata app update`| 更新应用程序。 |

可以获取有关 `--help` 参数的帮助，如以下示例中所示：

```bash
azdata app create --help
```

下面各部分详细说明了这些参数。

## <a name="sign-in"></a>登录

在部署应用程序或与应用程序交互之前，请先通过 `azdata login` 命令登录到 SQL Server 大数据群集。 指定 `controller-svc-external` 服务的外部 IP 地址（例如：`https://ip-address:30080`）以及群集的用户名和密码。

```bash
azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

如果使用 AKS，则需要运行以下命令以获取 `controller-svc-external` 服务的 IP 地址，方法是在 bash 或 cmd 窗口中运行以下命令：


```bash
kubectl get svc controller-svc-external -n <name of your big data cluster>
```

## <a name="kubernetes-clusters-created-with-kubeadm"></a>使用 kubeadm 创建的 Kubernetes 群集

运行以下命令以获取用于登录到群集的 IP 地址

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>创建应用

若要创建应用程序，请结合使用 `azdata` 和 `app create` 命令。 这些文件位于创建应用的计算机本地。

使用以下语法在大数据群集中创建新应用：

```bash
azdata app create --spec <directory containing spec file>
```

以下命令举例说明了此命令的外观：

```bash
azdata app create --spec ./addpy
```

这假设你的应用程序存储在 `addpy` 文件夹中。 此文件夹还应包含应用程序的规范文件 `spec.yaml`。 有关 `spec.yaml` 文件的详细信息，请参阅[“应用程序部署”页](concept-application-deployment.md)。

要部署此应用示例应用，请在名为 `addpy` 的目录中创建以下文件：

- `add.py` 列中的一个值匹配。 将以下 Python 代码复制到此文件中：
   ```py
   #add.py
  def add(x, y):
    result = x+y
    return result
  result=add(x,y)
   ```
- `spec.yaml` 列中的一个值匹配。 将以下代码复制到此文件中：
   ```yaml
   #spec.yaml
   name: add-app #name of your python script
   version: v1  #version of the app
   runtime: Python #the language this app uses (R or Python)
   src: ./add.py #full path to the location of the app
   entrypoint: add #the function that will be called upon execution
   replicas: 1  #number of replicas needed
   poolsize: 1  #the pool size that you need your app to scale
   inputs:  #input parameters that the app expects and the type
     x: int
     y: int
   output: #output parameter the app expects and the type
     result: int
   ```

然后，运行以下命令：

```bash
azdata app create --spec ./addpy
```

可以使用 list 命令检查是否部署了该应用：

```bash
azdata app list
```

如果部署未完成，应会看到 `state` 显示为 `WaitingforCreate`，如以下示例所示：

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

部署成功后，应会看到 `state` 更改为 `Ready` 状态：

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>列出应用

可以列出通过 `app list` 命令成功创建的任何应用。

以下命令列出了大数据群集中所有可用的应用程序：

```bash
azdata app list
```

如果指定名称和版本，则会列出该特定应用及其状态（“正在创建”或“就绪”）：

```bash
azdata app list --name <app_name> --version <app_version>
```

下面的示例对此命令进行了演示：

```bash
azdata app list --name add-app --version v1
```

应会看到与如下示例类似的输出：

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>运行应用

如果应用处于 `Ready` 状态，则可以使用指定的输入参数运行它。 使用以下语法运行应用：

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

下面的示例命令演示了 run 命令：

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

如果运行成功，应会看到创建应用时所指定的输出。 下面是一个示例。

```json
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```

## <a name="create-an-app-skeleton"></a>创建应用主干

Init 命令为基架提供部署应用程序所需的相关生成工件。 下面的示例创建 hello，可通过运行以下命令来执行此操作。

```bash
azdata app init --name hello --version v1 --template python
```

这将创建一个名为 hello 的文件夹。  可以使用 `cd` 进入目录并检查文件夹中生成的文件。 spec.yaml 定义应用，如名称、版本和源代码。 可以编辑该规范以更改名称、版本、输入和输出。

下面是将在文件夹中看到的 init 命令的示例输出

```
hello.py
run-spec.yaml
spec.yaml
```

## <a name="describe-an-app"></a>描述应用

describe 命令提供有关应用程序的详细信息，包括群集中的终结点。 应用开发人员通常使用此命令通过 swagger 客户端来生成应用，并使用 Web 服务以 RESTful 的方式与应用进行交互。 有关详细信息，请参阅[在大数据群集上使用应用程序](big-data-cluster-consume-apps.md)。

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30080/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30080/api/app/add-app/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

## <a name="delete-an-app"></a>删除应用

要从大数据群集中删除应用，请使用以下语法：

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>后续步骤

如需了解如何将部署在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 上的应用集成到自己的应用程序中，请参阅[使用大数据群集上的应用程序](big-data-cluster-consume-apps.md)获取详细信息。 有关其他示例，请参阅[应用部署示例](https://aka.ms/sql-app-deploy)。

有关 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
