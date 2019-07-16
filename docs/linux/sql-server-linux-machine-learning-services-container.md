---
title: 运行 SQL Server 机器学习服务在容器中的 |Microsoft Docs
description: 本教程演示如何使用 SQL Server 机器学习服务中的 Linux 容器在 Docker 上运行。
author: uc-msft
ms.author: umajay
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
moniker: '>= sql-server-linux-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 484f4fc9e51bc8d6ec4ad6e2e75df88593672c28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941085"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>运行 SQL Server 机器学习服务在容器中

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教程演示如何生成具有 SQL Server 机器学习服务的 Docker 容器并运行 Transact SQL 从机器学习脚本。

> [!div class="checklist"]
> * Mssql docker 存储库克隆。
> * 生成包含机器学习服务的 SQL Server Linux 容器映像。
> * 使用机器学习服务中运行 SQL Server Linux 容器映像。
> * 运行 R 或 Python 脚本使用 TRANSACT-SQL 语句。
> * 停止并删除 SQL Server Linux 容器。 

## <a name="prerequisites"></a>先决条件

* Git 命令行接口。
* 适用于支持的任一 Linux 分发版的 Docker 引擎 1.8 以上版本，或适用于 Mac/Windows 的 Docker。 有关详细信息，请参阅 [Install Docker](https://docs.docker.com/engine/installation/)（安装 Docker）。
* 2 gb 的磁盘空间最小值。
* 2 GB 的 RAM 的最小值。
* [Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

## <a name="clone-the-mssql-docker-repository"></a>Mssql docker 存储库克隆

1. 打开 bash 终端上在 Windows 上的 Linux/Mac 或 WSL 终端。

1. 创建用于本地保存一份 mssql docker 存储库的本地目录。
1. 运行 git 克隆命令克隆 mssql docker 存储库。

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-sql-server-linux-container-image-with-machine-learning-services"></a>生成包含机器学习服务的 SQL Server Linux 容器映像

1. 将目录更改为 mssql mlservices 目录。

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. 执行 build.sh 脚本。

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > 生成 docker 映像，则需要安装包的几个 Gb 的大小。 该脚本可能需要 20 分钟才能完成，具体取决于网络带宽。

## <a name="run-sql-server-linux-container-image-with-machine-learning-services"></a>使用机器学习服务运行 SQL Server Linux 容器映像

1. 在运行该容器之前设置环境变量。 PATH_TO_MSSQL 环境变量设置为主机目录。

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

   此命令创建 SQL Server 容器与机器学习服务开发人员版 （默认值）。 SQL Server 端口**1433年**作为端口在主机上公开**1401年**。

   > [!NOTE]
   > 在容器中运行生产 SQL Server 版本的过程是略有不同。 有关详细信息，请参阅[运行生产容器映像](sql-server-linux-configure-docker.md#production)。 如果使用相同的容器名称和端口，本演练的其余部分仍适用生产容器。

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

## <a name="execute-r--python-scripts-from-transact-sql"></a>执行 R / Python 脚本从 TRANSACT-SQL

1. 连接到容器中的 SQL Server，并通过运行以下 T-SQL 语句来启用外部脚本配置选项。

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. 验证通过运行以下简单的 R/Python sp_execute_external_script 工作机器学习服务。

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

本教程介绍如何执行以下操作：

> [!div class="checklist"]
> * Mssql docker 存储库克隆。
> * 生成包含机器学习服务的 SQL Server Linux 容器映像。
> * 使用机器学习服务中运行 SQL Server Linux 容器映像。
> * 运行 R 或 Python 脚本使用 TRANSACT-SQL 语句。
> * 停止并删除 SQL Server Linux 容器。

接下来，查看其他 Docker 配置和故障排除方案：

> [!div class="nextstepaction"]
>[Docker 上的 SQL Server 的配置指南](sql-server-linux-configure-docker.md)
