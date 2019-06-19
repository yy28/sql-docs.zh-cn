---
title: 脱机部署
titleSuffix: SQL Server big data clusters
description: 了解如何执行的 SQL Server 大数据群集脱机部署。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fd6a1e1e6f2ad661c8a2316c434854095c7f6da5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797891"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>执行 SQL Server 大数据群集的脱机部署

本文介绍如何执行 SQL Server 2019 大数据群集 （预览版） 的脱机部署。 大数据群集必须能够访问 Docker 存储库从中拉取容器映像。 脱机安装是一个所需的图像放置到专用 Docker 存储库的位置。 该专用存储库然后用作新的部署映像源。

## <a name="prerequisites"></a>先决条件

- 适用于支持的任一 Linux 分发版的 Docker 引擎 1.8 以上版本，或适用于 Mac/Windows 的 Docker。 有关详细信息，请参阅 [Install Docker](https://docs.docker.com/engine/installation/)（安装 Docker）。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>将图像加载到专用存储库

以下步骤介绍如何从 Microsoft 存储库拉取大数据群集的容器映像并将其推送到专用存储库。

> [!TIP]
> 以下步骤介绍该过程。 但是，若要简化任务，可以使用[自动化脚本](#automated)而不是手动运行这些命令。

1. 首先，登录到 Microsoft Docker 注册表**docker 登录**命令。 提供给您作为早期采用计划的一部分，Microsoft 使用的用户名和密码。

   ```PowerShell
   docker login private-repo.microsoft.com -u  <SOURCE_DOCKER_USERNAME> -p <SOURCE_DOCKER_PASSWORD>
   ```

   > [!TIP]
   > 这些命令使用 PowerShell 为例，但是您可以从 cmd、 bash 或任何命令行界面，可以运行 docker 运行它们。 在 Linux 上，添加`sudo`到每个命令。

1. 通过重复以下命令来提取大数据群集容器映像。 替换`<SOURCE_IMAGE_NAME>`与每个[映像名称](#images)。 替换`<SOURCE_DOCKER_TAG>`与适用于大数据标记群集版本中，如**ctp3.0**。  

   ```PowerShell
   docker pull private-repo.microsoft.com/mssql-private-preview/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. 登录到在目标私有 Docker 注册表。

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. 标记使用以下命令为每个图像的本地映像：

   ```PowerShell
   docker tag private-repo.microsoft.com/mssql-private-preview/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. 将本地映像推送到专用 Docker 存储库：

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a> 大数据群集容器映像

以下大数据群集容器映像所需的脱机安装：

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
 - **mssql-java**
 - **mssql-mlservices-pythonserver**
 - **mssql-mlservices-rserver**
 - **mssql-monitor-elasticsearch**
 - **mssql-monitor-influxdb**
 - **mssql-security-knox**
 - **mssql-mlserver-r-runtime**
 - **mssql-mlserver-py-runtime**
 - **mssql-controller**
 - **mssql-portal**
 - **mssql-server-controller**
 - **mssql-monitor-grafana**
 - **mssql-monitor-kibana**
 - **mssql-service-proxy**
 - **mssql-app-service-proxy**
 - **mssql-ssis-app-runtime**
 - **mssql-monitor-telegraf**

## <a id="automated"></a> 自动执行的脚本

可以使用自动化的 python 脚本将自动提取所有必需的容器映像并将它们推送到专用存储库。

> [!NOTE]
> Python 是使用脚本的先决条件。 有关如何安装 Python 的详细信息，请参阅[Python 文档](https://wiki.python.org/moin/BeginnersGuide/Download)。

1. 从 bash 或 PowerShell，下载的脚本**curl**:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. 然后运行该脚本使用以下命令之一：

   **Windows:**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **Linux:**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. 按照用于输入 Microsoft 存储库和专用存储库信息提示。 在脚本完成后，所有必需的映像应位于专用存储库。

## <a name="install-tools-offline"></a>安装脱机工具

大数据群集部署需要几个工具，包括**Python**， **mssqlctl**，并**kubectl**。 使用以下步骤以在脱机服务器上安装这些工具。

### <a id="python"></a> 安装 python 脱机

1. 在具有 internet 访问计算机上，下载以下压缩文件包含 Python 之一：

   | 操作系统 | 下载 |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. 将压缩的文件复制到目标计算机并将其解压缩到所选的文件夹。

1. 对于 Windows，运行`installLocalPythonPackages.bat`从该文件夹并到相同的文件夹作为参数传递的完整路径。

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="mssqlctl"></a> 安装脱机 mssqlctl

1. 具有 internet 访问的计算机上并[Python](https://wiki.python.org/moin/BeginnersGuide/Download)，运行以下命令以下载所有关闭**mssqlctl**程序包添加到当前文件夹。

   ```PowerShell
   pip download -r https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt
   ```

1. 下载**requirements.txt**文件。

   ```PowerShell
   curl -o requirements.txt "https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt"
   ```

1. 将下载的包和**requirements.txt**到目标计算机的文件。

1. 指定复制到以前的文件的文件夹在目标计算机上运行以下命令。

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a> 安装 kubectl 脱机

若要安装**kubectl**到脱机计算机，请使用以下步骤。

1. 使用**curl**若要下载**kubectl**到所选的文件夹。 有关详细信息，请参阅[安装 kubectl 二进制文件使用 curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)。

1. 将文件夹复制到目标计算机。

## <a name="deploy-from-private-repository"></a>从专用存储库进行部署

若要从专用存储库部署，请使用中所述的步骤[部署指南](deployment-guidance.md)，但使用自定义部署配置文件，指定你的私有 Docker 存储库信息。 以下**mssqlctl**命令演示如何更改名为的自定义部署配置文件中的 Docker 设置**custom.json**:

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.docker.repository=<your-docker-repository>"
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.docker.registry=<your-docker-registry>"
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.docker.imageTag=<your-docker-image-tag>"
```

部署会提示您输入 docker 用户名和密码，也可以指定在**DOCKER_USERNAME**并**DOCKER_PASSWORD**环境变量。

## <a name="next-steps"></a>后续步骤

有关大数据群集部署的详细信息，请参阅[如何部署 SQL Server 大数据群集在 Kubernetes 上](deployment-guidance.md)。
