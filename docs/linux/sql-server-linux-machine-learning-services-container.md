---
title: 在容器中运行 SQL Server 机器学习服务 | Microsoft Docs
description: 本教程介绍如何在 Docker 上运行的 Linux 容器中使用 SQL Server 机器学习服务。
author: uc-msft
ms.author: umajay
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
moniker: '>= sql-server-linux-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: f3d3774adf4bee07269b25c3359b031ca24eb99e
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68300427"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>在容器中运行 SQL Server 机器学习服务

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教程演示如何通过 SQL Server 机器学习服务生成 Docker 容器，并运行 Transact-SQL 中的机器学习脚本。

> [!div class="checklist"]
> * 克隆 mssql-docker 存储库。
> * 通过机器学习服务生成 SQL Server Linux 容器映像。
> * 通过机器学习服务运行 SQL Server Linux 容器映像。
> * 使用 Transact-SQL 语句运行 R 或 Python 脚本。
> * 停止和删除 SQL Server Linux 容器。 

## <a name="prerequisites"></a>必备条件

* Git 命令行接口。
* 任何受支持的 Linux 分发版上或用于 Mac/Windows 的 Docker 上的 Docker 引擎 1.8+。 有关详细信息，请参阅 [Install Docker](https://docs.docker.com/engine/installation/)（安装 Docker）。
* 至少 2 GB 的磁盘空间。
* 至少 2 GB 的 RAM。
* [Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

## <a name="clone-the-mssql-docker-repository"></a>克隆 mssql-docker 存储库

1. 在 Linux/Mac 上打开 bash 终端，或在 Windows 上打开 WSL 终端。

1. 创建本地目录以在本地存放 mssql docker 存储库的副本。
1. 运行 git 克隆命令以克隆 mssql-docker 存储库。

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-sql-server-linux-container-image-with-machine-learning-services"></a>通过机器学习服务生成 SQL Server Linux 容器映像

1. 将目录更改为 mssql-mlservices 目录。

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. 执行 build.sh 脚本。

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > 生成 docker 映像需要安装大小为多个 GB 的包。 此脚本可能需要长达 20 分钟的时间才能完成，具体取决于网络带宽。

## <a name="run-sql-server-linux-container-image-with-machine-learning-services"></a>通过机器学习服务运行 SQL Server Linux 容器映像

1. 运行容器之前设置环境变量。 将 PATH_TO_MSSQL 环境变量设置为主机目录。

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. 执行 run.sh 脚本。

   ```bash
   ./run.sh
   ```

   此命令通过开发人员版机器学习服务创建 SQL Server 容器（默认）。 SQL Server 端口 1433 作为端口 1401 在主机上公开   。

   > [!NOTE]
   > 在容器中运行生产 SQL Server 版本的过程略有不同。 有关详细信息，请参阅 [在 Docker 上配置 SQL Server 容器映像](sql-server-linux-configure-docker.md)。 如果使用相同的容器名称和端口，本教程的其余部分仍适用于生产容器。

1. 要查看 Docker 容器，请使用 `docker ps` 命令。

   ```bash
   sudo docker ps -a
   ```

1. 如果“状态”列显示“正常运行”，则 SQL Server 将在容器中运行，并侦听“端口”列中指定的端口    。 如果 SQL Server 容器的“状态”列显示“已退出”，则参阅[配置指南的疑难解答部分](sql-server-linux-configure-docker.md#troubleshooting)   。

   ```bash
   $ sudo docker ps -a
   ```

    输出： 
    
    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="change-the-sa-password"></a>更改 SA 密码

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="execute-r--python-scripts-from-transact-sql"></a>使用 Transact-SQL 语句执行 R/Python 脚本

1. 通过运行以下 T-SQL 语句连接到容器中的 SQL Server，并启用外部脚本配置选项。

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. 运行以下简单的 R/Python sp_execute_external_script，验证机器学习服务是否正常运行。

    ```sql
    execute sp_execute_external_script 
    @language = N'R',
    @script = N'
    print("Hello World!")
    print(R.version)
    print(Revo.version)
    OutputDataSet <- InputDataSet', 
    @input_data_1 = N'select 1'
    with result sets((i int));
    go
    ```

    ```sql
    execute sp_execute_external_script 
    @language = N'Python',
    @script = N'
    import sys
    print(sys.version)
    print("Hello World!")
    OutputDataSet = InputDataSet',
    @input_data_1 = N'select 1'
    with result sets((i int));
    go 
    ```

## <a name="next-steps"></a>后续步骤

在本教程中，你已学习如何执行以下操作：

> [!div class="checklist"]
> * 克隆 mssql-docker 存储库。
> * 通过机器学习服务生成 SQL Server Linux 容器映像。
> * 通过机器学习服务运行 SQL Server Linux 容器映像。
> * 使用 Transact-SQL 语句运行 R 或 Python 脚本。
> * 停止和删除 SQL Server Linux 容器。

接下来，查看其他 Docker 配置和故障排除方案：

> [!div class="nextstepaction"]
>[Docker 上的 SQL Server 配置指南](sql-server-linux-configure-docker.md)
