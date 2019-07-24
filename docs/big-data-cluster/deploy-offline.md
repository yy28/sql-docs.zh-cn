---
title: 脱机部署
titleSuffix: SQL Server big data clusters
description: 了解如何执行 SQL Server 大数据群集的脱机部署。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cd8b3128fc11037a5ade494813611d473c995f8f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419366"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>执行 SQL Server 大数据群集的脱机部署

本文介绍如何执行 SQL Server 2019 大数据群集 (预览版) 的脱机部署。 大数据群集必须有权访问要从中提取容器映像的 Docker 存储库。 脱机安装是指将所需的映像置于专用 Docker 存储库中。 然后, 将该专用存储库用作新部署的图像源。

## <a name="prerequisites"></a>先决条件

- 适用于支持的任一 Linux 分发版的 Docker 引擎 1.8 以上版本，或适用于 Mac/Windows 的 Docker。 有关详细信息，请参阅 [Install Docker](https://docs.docker.com/engine/installation/)（安装 Docker）。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>将映像加载到专用存储库

以下步骤介绍了如何从 Microsoft 存储库中拉取大数据群集容器映像, 然后将它们推送到专用存储库中。

> [!TIP]
> 以下步骤说明了该过程。 但是, 若要简化任务, 可以使用[自动脚本](#automated), 而不是手动运行这些命令。

1. 通过重复以下命令拉取大数据群集容器映像。 替换`<SOURCE_IMAGE_NAME>`为每个[映像名称](#images)。 将`<SOURCE_DOCKER_TAG>`替换为大数据群集版本的标记, 例如**2019-ctp 3.2-ubuntu**。  

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. 登录到目标专用 Docker 注册表。

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. 对于每个映像, 用以下命令标记本地映像:

   ```PowerShell
   docker tag mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. 将本地映像推送到专用 Docker 存储库:

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a>大数据群集容器映像

脱机安装需要以下大数据群集容器映像:

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
 - **mssql-monitor-elasticsearch**
 - **mssql-monitor-influxdb**
 - **mssql-security-knox**
 - **mssql-mlserver-r-runtime**
 - **mssql-mlserver-py-runtime**
 - **mssql-controller**
 - **mssql-server-controller**
 - **mssql-monitor-grafana**
 - **mssql-monitor-kibana**
 - **mssql-service-proxy**
 - **mssql-app-service-proxy**
 - **mssql-ssis-app-runtime**
 - **mssql-monitor-telegraf**
 - **mssql-mleap-serving-runtime**
 - **mssql-安全支持**

## <a id="automated"></a>自动脚本

你可以使用自动化的 python 脚本, 该脚本将自动提取所有必需的容器映像并将其推送到专用存储库中。

> [!NOTE]
> Python 是使用该脚本的先决条件。 有关如何安装 Python 的详细信息, 请参阅[python 文档](https://wiki.python.org/moin/BeginnersGuide/Download)。

1. 从 bash 或 PowerShell 下载带**卷**的脚本:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. 然后, 用以下命令之一运行该脚本:

   **Windows**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **Linux**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. 按照提示输入 Microsoft 存储库和专用存储库信息。 脚本完成后, 所有所需的映像都应位于你的专用存储库中。

## <a name="install-tools-offline"></a>脱机安装工具

大数据群集部署需要多种工具, 包括**Python**、 **azdata**和**kubectl**。 使用以下步骤在脱机服务器上安装这些工具。

### <a id="python"></a>脱机安装 python

1. 在具有 internet 访问权限的计算机上, 下载以下包含 Python 的压缩文件之一:

   | 操作系统 | 下载 |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. 将压缩文件复制到目标计算机, 并将其解压缩到所选的文件夹。

1. 仅适用于 Windows, `installLocalPythonPackages.bat`从该文件夹运行并将完整路径传递到与参数相同的文件夹。

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="azdata"></a>脱机安装 azdata

1. 在具有 internet 访问权限的计算机[上, 运行](https://wiki.python.org/moin/BeginnersGuide/Download)以下命令, 将所有**azdata**包下载到当前文件夹。

   ```PowerShell
   pip download -r https://aka.ms/azdata
   ```

1. 将下载的包和**要求 .txt**文件复制到目标计算机。

1. 在目标计算机上运行以下命令, 并指定将以前的文件复制到其中的文件夹。

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a>脱机安装 kubectl

若要将**kubectl**安装到脱机计算机, 请使用以下步骤。

1. 使用 "**卷**" 将**kubectl**下载到所选的文件夹。 有关详细信息, 请参阅[使用卷安装 kubectl 二进制文件](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)。

1. 将文件夹复制到目标计算机。

## <a name="deploy-from-private-repository"></a>从专用存储库部署

若要从专用存储库进行部署, 请使用[部署指南](deployment-guidance.md)中所述的步骤, 但使用指定专用 Docker 存储库信息的自定义部署配置文件。 以下**azdata**命令演示如何**在名为**的自定义部署配置文件中更改 Docker 设置:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.repository=<your-docker-repository>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.registry=<your-docker-registry>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.imageTag=<your-docker-image-tag>"
```

部署会提示你提供 docker 用户名和密码, 或者可以在**DOCKER_USERNAME**和**DOCKER_PASSWORD**环境变量中指定它们。

## <a name="next-steps"></a>后续步骤

有关大数据群集部署的详细信息, 请参阅[如何在 Kubernetes 上部署 SQL Server 大数据群集](deployment-guidance.md)。
