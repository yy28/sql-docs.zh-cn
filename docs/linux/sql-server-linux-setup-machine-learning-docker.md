---
title: 在 Docker 上安装
titleSuffix: SQL Server Machine Learning Services
description: 了解如何在 Docker 上安装 SQL Server 机器学习服务（Python 和 R）。
author: cawrites
ms.author: chadam
ms.reviewer: davidph
manager: cgronlun
ms.date: 03/23/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: eb42a3b63c06e1d436bfac8f727c87ce201bd4ec
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664379"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-docker"></a>在 Docker 上安装 SQL Server 机器学习服务（Python 和 R）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Docker 上安装 SQL Server 机器学习服务。 可使用机器学习服务在数据库中执行 Python 和 R 脚本。 我们不为预建容器提供机器学习服务。 你可以使用 [GitHub 上的可用示例模板](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)在 SQL Server 容器中创建一个。

## <a name="prerequisites"></a>先决条件

- Git 命令行接口。

- 任何受支持的 Linux 发行版本上的 Docker 引擎 1.8 及更高版本，或用于 Mac/Windows 的 Docker。 有关详细信息，请参阅[了解 Docker](https://docs.docker.com/get-docker/)。

- 另请参阅 [Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

## <a name="clone-the-mssql-docker-repository"></a>克隆 mssql-docker 存储库

以下命令将 `mssql-docker` git 存储库克隆到本地目录。

1. 在 Linux 或 Mac 上打开 Bash 终端，或在 Windows 上打开适用于 Linux 的 Windows 子系统终端。

2. 创建一个目录来保存 mssql-docker 存储库的本地副本。

3. 运行 git clone 命令，以克隆 mssql-docker 存储库：

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image"></a>构建 SQL Server Linux 容器映像

完成以下步骤以生成 docker 映像：

1. 将目录更改为 mssql-mlservices 目录：

2. 在同一目录中，运行以下命令：

    ```bash
    docker builds -t mssql-server-mlservices
    ```

3. 运行以下命令：

    ```bash
    docker runs -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e SA_PASSWORD=<your_sa_password> -v OS>:/var/opt/mssql -p 1433:1433 mssql-server-mlservices
    ```

    更改 `SA_PASSWORD=<your_sa_password>` 中的 `<your_sa_password>` 并更改 `-v` 路径。 

4. 通过运行以下命令进行确认：

    ```bash
    docker ps -a
    ```

   > [!NOTE]
   > 必须安装几个 GB 大小的包，才能生成 Docker 映像。 此脚本可能需要一段时间才能完成运行，具体视网络带宽而定。

## <a name="run-the-sql-server-linux-container-image"></a>运行 SQL Server Linux 容器映像

1. 先设置环境变量，再运行容器。 将 PATH_TO_MSSQL 环境变量设置为主机目录：

   ```bash
   export MSSQL_PID='Developer'
   export ACCEPT_EULA='Y'
   export ACCEPT_EULA_ML='Y'
   export PATH_TO_MSSQL='/home/mssql/'
   ```

2. 运行 run.sh 脚本：

   ```bash
   ./run.sh
   ```

   此命令使用开发人员版（默认）机器学习服务创建 SQL Server 容器。 SQL Server 端口 1433 在主机上公开为端口 1401   。

   > [!NOTE]
   > 在容器中运行 SQL Server 生产版本的过程略有不同。 有关详细信息，请参阅 [在 Docker 上配置 SQL Server 容器映像](sql-server-linux-configure-docker.md)。 如果使用相同的容器名称和端口，本教程的其余部分仍适用于生产容器。

3. 若要查看 Docker 容器，请运行 `docker ps` 命令：

   ```bash
   sudo docker ps -a
   ```

4. 如果“状态”  列显示“正常运行”  状态，表明 SQL Server 正在容器中运行，且正在侦听“端口”  列中指定的端口。 如果 SQL Server 容器的“状态”列显示“已退出”，则参阅[配置指南的疑难解答部分](sql-server-linux-configure-docker.md#troubleshooting)   。

   ```bash
   $ sudo docker ps -a
   ```

    输出：

    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="enable-machine-learning-services"></a>启用机器学习服务

若要启用机器学习服务，请连接到 SQL Server 实例，并运行以下 T-SQL 语句：

```sql
EXEC sp_configure  'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE
```

## <a name="next-steps"></a>后续步骤

Python 开发人员可以通过以下教程了解如何将 Python 与 SQL Server 一起使用：

+ [Python 教程：在 SQL Server 机器学习服务中使用线性回归来预测雪橇租赁](../machine-learning/tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Python 教程：配合使用 K-Means 群集和 SQL Server 机器学习服务对客户进行分类](../machine-learning/tutorials/python-clustering-model.md)

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 协同工作的基础知识。 有关下一步，请参阅以下链接：

+ [快速入门：在 T-SQL 中运行 R](../machine-learning/tutorials/quickstart-r-create-script.md)
+ [教程：适用于 R 开发人员的数据库内分析](../machine-learning/tutorials/sqldev-in-database-r-for-sql-developers.md)
