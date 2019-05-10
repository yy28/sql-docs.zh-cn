---
title: 使用 mssqlctl 部署应用程序
titleSuffix: SQL Server big data clusters
description: 将 Python 或 R 脚本部署为 SQL Server 2019 大数据群集 （预览版） 上的应用程序。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 5953b5b36639438d80805bfb3dacc850d8c67dce
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775368"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-cluster-preview"></a>如何部署 SQL Server 大数据群集 （预览版） 上的应用程序

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何部署和管理 R 和 Python 脚本为 SQL Server 2019 大数据群集 （预览版） 内的应用程序。

## <a name="whats-new-and-improved"></a>新增功能和改进

- 用于管理群集和应用程序的单个命令行实用工具。
- 简化应用程序部署，同时通过规范文件提供精细的控制。
- 支持托管其他应用程序类型的 SSIS 和 MLeap （中的新增功能 CTP 2.3)
- [VS Code 扩展](app-deployment-extension.md)来管理应用程序部署

应用程序部署和管理使用`mssqlctl`命令行实用程序。 本文提供有关如何从命令行部署应用程序的示例。 若要了解如何使用 Visual Studio Code 中这指[VS Code 扩展](app-deployment-extension.md)。

支持以下类型的应用：
- R 和 Python 应用 （函数、 模型和应用）
- MLeap 服务
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>先决条件

- [SQL Server 2019 大数据群集](deployment-guidance.md)
- [mssqlctl 命令行实用程序](deploy-install-mssqlctl.md)

## <a name="capabilities"></a>功能

在 SQL Server 2019 （预览版） ctp 版本 2.5 可以创建、 删除、 描述、 初始化，列表运行，并更新你的应用程序。 下表描述了可用于应用程序部署命令**mssqlctl**。

|Command |Description |
|:---|:---|
|`mssqlctl login` | 登录到 SQL Server 大数据群集 |
|`mssqlctl app create` | 创建应用程序。 |
|`mssqlctl app delete` | 删除应用程序。 |
|`mssqlctl app describe` | 介绍应用程序。 |
|`mssqlctl app init` | 启动新应用程序框架。 |
|`mssqlctl app list` | 列出应用程序。 |
|`mssqlctl app run` | 运行应用程序。 |
|`mssqlctl app update`| 更新应用程序。 |

可以获取帮助`--help`参数，如以下示例所示：

```bash
mssqlctl app create --help
```

以下部分介绍这些命令的更多详细信息。

## <a name="sign-in"></a>登录

在部署或与应用程序进行交互之前，先登录到 SQL Server 使用的大数据群集`mssqlctl login`命令。 指定的外部 IP 地址`mgmtproxy-svc-external`服务 (例如： `https://ip-address:30777`) 以及用户名和密码向群集。

```bash
mssqlctl login -e https://<ip-address-of-mgmtproxy-svc-external>:30777 -u <user-name> -p <password>
```

## <a name="aks"></a>AKS

如果使用 AKS 时，需要运行以下命令以获取的 IP 地址`mgmtproxy-svc-external`服务通过在 bash 或 cmd 窗口中运行以下命令：


```bash
kubectl get svc mgmtproxy-svc-external -n <name of your cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm 或 Minikube

如果使用 Kubeadm 或 Minikube 运行以下命令以获取到群集中的登录名的 IP 地址

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>创建应用

若要创建的应用程序，请使用`mssqlctl`与`app create`命令。 这些文件创建从应用的计算机上驻留在本地。

使用以下语法在大数据群集中创建新的应用程序：

```bash
mssqlctl app create --spec <directory containing spec file>
```

以下命令显示了此命令可能如下所示的示例：

```bash
mssqlctl app create --spec ./addpy
```

这假定你已存储在应用程序`addpy`文件夹。 此文件夹还应包含名为被调用应用程序的规范文件`spec.yaml`。 请参阅[应用程序部署页](concept-application-deployment.md)有关详细信息`spec.yaml`文件。

若要部署此应用程序示例应用，可在一个名为目录中创建以下文件`addpy`:

- `add.py` 的用户。 将以下 Python 代码复制到此文件：
   ```py
   #add.py
   def add(x,y):
        result = x+y
        return result
    result=add(x,y)
   ```
- `spec.yaml` 的用户。 将以下代码复制到此文件：
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
mssqlctl app create --spec ./addpy
```

你可以检查是否使用列表命令部署应用：

```bash
mssqlctl app list
```

如果部署未完成您应看到`state`显示`WaitingforCreate`如下面的示例：

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

部署成功后，你应看到`state`更改为`Ready`状态：

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

可以列出已成功创建了与任何应用`app list`命令。

以下命令列出了大数据群集中所有可用的应用程序：

```bash
mssqlctl app list
```

如果指定的名称和版本，它列出了该特定应用程序和其状态 （创建或就绪）：

```bash
mssqlctl app list --name <app_name> --version <app_version>
```

下面的示例演示了此命令：

```bash
mssqlctl app list --name add-app --version v1
```

应看到类似于下面的示例输出：

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

如果该应用位于`Ready`状态，则可以通过运行具有指定的输入参数使用它。 使用以下语法来运行应用：

```bash
mssqlctl app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

以下示例命令演示如何运行的命令：

```bash
mssqlctl app run --name add-app --version v1 --inputs x=1,y=2
```

如果成功运行，您应看到在输出与创建该应用程序时指定。 下面是一个示例。

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

## <a name="create-an-app-skeleton"></a>创建应用框架

Init 命令提供了部署应用程序需要使用相关的项目基架。 下面的示例创建你好，你可以通过运行以下命令来执行此操作。

```bash
mssqlctl app init --name hello --version v1 --template python
```

这将创建一个名为你好文件夹。  你可以`cd`到目录并检查生成的文件的文件夹中。 spec.yaml 定义应用程序中，如名称、 版本和源的代码。 您可以编辑规范来更改名称、 版本、 输入和输出。

下面是您将看到文件夹中的 init 命令的示例输出

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>描述应用程序

描述命令提供有关应用程序包括在群集中的终结点的详细的信息。 这通常用于由应用开发人员生成的应用程序使用 swagger 客户端和使用 web 服务与应用交互以 RESTful 方式。 请参阅[使用大数据群集上的应用程序](big-data-cluster-consume-apps.md)有关详细信息。

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
    "app": "https://10.1.1.3:30777/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30777/api/app/add-app/v1/swagger.json"
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

若要从大数据群集中删除应用，使用以下语法：

```bash
mssqlctl app delete --name add-app --version v1
```

## <a name="next-steps"></a>后续步骤

了解如何将大数据群集在您的应用程序的 SQL Server 上部署的应用程序进行集成[使用大数据群集上的应用程序](big-data-cluster-consume-apps.md)有关详细信息。 您还可以查看其他示例位于[应用程序部署示例](https://aka.ms/sql-app-deploy)。

有关 SQL Server 大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
