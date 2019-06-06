---
title: 在 Docker 中的将 SQL Server 数据库还原 |Microsoft Docs
description: 本教程演示如何还原新的 Linux Docker 容器中的 SQL Server 数据库备份。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: f688a95135716a41ae37cb86b50bcb90fc6cce5e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712814"
---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>在 Linux Docker 容器中的将 SQL Server 数据库还原

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

本教程演示如何移动和 SQL Server 备份文件还原到 SQL Server 2017 Linux 容器映像在 Docker 上运行。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

本教程演示如何移动和 SQL Server 备份文件还原到在 Docker 上运行 SQL Server 2019 预览 Linux 容器映像。

::: moniker-end

> [!div class="checklist"]
> * 请求和运行最新的 SQL Server Linux 容器映像。
> * Wide World Importers 数据库文件复制到容器。
> * 在容器中的将数据库还原。
> * 运行 TRANSACT-SQL 语句来查看和修改数据库。
> * 备份已修改的数据库。

## <a name="prerequisites"></a>先决条件

* 适用于支持的任一 Linux 分发版的 Docker 引擎 1.8 以上版本，或适用于 Mac/Windows 的 Docker。 有关详细信息，请参阅 [Install Docker](https://docs.docker.com/engine/installation/)（安装 Docker）。
* 至少 2 GB 的磁盘空间
* 至少 2 GB 的 RAM
* [Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

## <a name="pull-and-run-the-container-image"></a>请求和运行容器映像

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 打开 bash 终端在 Linux/Mac 上的或在 Windows 上提升的 PowerShell 会话。

1. 从 Docker Hub 中拉出 SQL Server 2017 Linux 容器映像。

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!TIP]
   > 在本教程中，整个 docker 命令给出了示例 bash shell (Linux/Mac) 和 PowerShell (Windows)。

1. 要通过 Docker 运行容器映像，可使用下列命令：

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   此命令创建 SQL Server 2017 容器与开发人员版 （默认值）。 SQL Server 端口**1433年**作为端口在主机上公开**1401年**。 可选`-v sql1data:/var/opt/mssql`参数创建一个名为的数据卷容器**sql1ddata**。 这用于保存 SQL Server 创建的数据。

   > [!NOTE]
   > 在容器中运行生产 SQL Server 版本的过程是略有不同。 有关详细信息，请参阅[运行生产容器映像](sql-server-linux-configure-docker.md#production)。 如果使用相同的容器名称和端口，本演练的其余部分仍适用生产容器。

1. 要查看 Docker 容器，请使用 `docker ps` 命令。

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. 如果“状态”列显示“正常运行”，则 SQL Server 将在容器中运行，并侦听“端口”列中指定的端口    。 如果 SQL Server 容器的“状态”列显示“已退出”，则参阅[配置指南的疑难解答部分](sql-server-linux-configure-docker.md#troubleshooting)   。

  ```bash
  $ sudo docker ps -a

  CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
  941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
  ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 打开 bash 终端在 Linux/Mac 上的或在 Windows 上提升的 PowerShell 会话。

1. 从 Docker 中心请求 SQL Server 2019 预览 Linux 容器映像。

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   > [!TIP]
   > 在本教程中，整个 docker 命令给出了示例 bash shell (Linux/Mac) 和 PowerShell (Windows)。

1. 要通过 Docker 运行容器映像，可使用下列命令：

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   此命令创建 SQL Server 2019 预览版容器与开发人员版 （默认值）。 SQL Server 端口**1433年**作为端口在主机上公开**1401年**。 可选`-v sql1data:/var/opt/mssql`参数创建一个名为的数据卷容器**sql1ddata**。 这用于保存 SQL Server 创建的数据。

1. 要查看 Docker 容器，请使用 `docker ps` 命令。

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. 如果“状态”列显示“正常运行”，则 SQL Server 将在容器中运行，并侦听“端口”列中指定的端口    。 如果 SQL Server 容器的“状态”列显示“已退出”，则参阅[配置指南的疑难解答部分](sql-server-linux-configure-docker.md#troubleshooting)   。

   ```bash
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

::: moniker-end

## <a name="change-the-sa-password"></a>更改 SA 密码

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>将备份文件复制到容器

本教程使用[Wide World Importers 示例数据库](../sample/world-wide-importers/wide-world-importers-documentation.md)。 使用以下步骤来下载并将 Wide World Importers 数据库备份文件复制到 SQL Server 容器。

1. 首先，使用**docker exec**创建备份文件夹。 以下命令将创建 **/var/opt/mssql/backup**目录内的 SQL Server 容器。

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. 接下来，下载[Wideworldimporters-full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0)到主机文件。 以下命令导航到主页/用户目录并下载备份文件作为**wwi.bak**。

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. 使用**docker cp**若要将备份文件复制到的容器中 **/var/opt/mssql/backup**目录。

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>还原数据库

备份文件现在位于容器内。 在还原之前备份，它是必须知道的逻辑文件名称和在备份的文件类型。 以下 TRANSACT-SQL 命令检查备份和还原使用执行**sqlcmd**容器中。

> [!TIP]
> 本教程使用**sqlcmd**的容器中，因为容器附带了预安装此工具。 但是，您也可以运行 TRANSACT-SQL 语句与其他客户端在容器外的工具如[Visual Studio Code](sql-server-linux-develop-use-vscode.md)或[SQL Server Management Studio](sql-server-linux-manage-ssms.md)。 若要连接，请使用已映射到容器中的端口 1433年的主机端口。 在此示例中，这是**localhost，1401年**在主机上并**Host_IP_Address，1401年**远程。

1. 运行**sqlcmd**列出逻辑文件名和路径在备份容器内。 这通过**RESTORE FILELISTONLY** TRANSACT-SQL 语句。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost \
      -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE FILELISTONLY FROM DISK = "/var/opt/mssql/backup/wwi.bak"' \
      | tr -s ' ' | cut -d ' ' -f 1-2
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost `
      -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/wwi.bak'"
   ```

   应看到类似于以下输出：

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. 调用**RESTORE DATABASE**命令在容器内的将数据库还原。 为每个文件上, 一步中指定新路径。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE DATABASE WideWorldImporters FROM DISK = "/var/opt/mssql/backup/wwi.bak" WITH MOVE "WWI_Primary" TO "/var/opt/mssql/data/WideWorldImporters.mdf", MOVE "WWI_UserData" TO "/var/opt/mssql/data/WideWorldImporters_userdata.ndf", MOVE "WWI_Log" TO "/var/opt/mssql/data/WideWorldImporters.ldf", MOVE "WWI_InMemory_Data_1" TO "/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE DATABASE WideWorldImporters FROM DISK = '/var/opt/mssql/backup/wwi.bak' WITH MOVE 'WWI_Primary' TO '/var/opt/mssql/data/WideWorldImporters.mdf', MOVE 'WWI_UserData' TO '/var/opt/mssql/data/WideWorldImporters_userdata.ndf', MOVE 'WWI_Log' TO '/var/opt/mssql/data/WideWorldImporters.ldf', MOVE 'WWI_InMemory_Data_1' TO '/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1'"
   ```

   应看到类似于以下输出：

   ```
   Processed 1464 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   Processed 33 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   Processed 3862 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Converting database 'WideWorldImporters' from version 852 to the current version 869.
   Database 'WideWorldImporters' running the upgrade step from version 852 to version 853.
   Database 'WideWorldImporters' running the upgrade step from version 853 to version 854.
   Database 'WideWorldImporters' running the upgrade step from version 854 to version 855.
   Database 'WideWorldImporters' running the upgrade step from version 855 to version 856.
   Database 'WideWorldImporters' running the upgrade step from version 856 to version 857.
   Database 'WideWorldImporters' running the upgrade step from version 857 to version 858.
   Database 'WideWorldImporters' running the upgrade step from version 858 to version 859.
   Database 'WideWorldImporters' running the upgrade step from version 859 to version 860.
   Database 'WideWorldImporters' running the upgrade step from version 860 to version 861.
   Database 'WideWorldImporters' running the upgrade step from version 861 to version 862.
   Database 'WideWorldImporters' running the upgrade step from version 862 to version 863.
   Database 'WideWorldImporters' running the upgrade step from version 863 to version 864.
   Database 'WideWorldImporters' running the upgrade step from version 864 to version 865.
   Database 'WideWorldImporters' running the upgrade step from version 865 to version 866.
   Database 'WideWorldImporters' running the upgrade step from version 866 to version 867.
   Database 'WideWorldImporters' running the upgrade step from version 867 to version 868.
   Database 'WideWorldImporters' running the upgrade step from version 868 to version 869.
   RESTORE DATABASE successfully processed 58455 pages in 18.069 seconds (25.273 MB/sec).
   ```

## <a name="verify-the-restored-database"></a>确认还原的数据库

运行以下查询以在容器中显示的数据库名称的列表：

```bash
sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
   -Q 'SELECT Name FROM sys.Databases'
```

```PowerShell
docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
   -Q "SELECT Name FROM sys.Databases"
```

应会看到**WideWorldImporters**中的数据库列表。

## <a name="make-a-change"></a>进行更改

以下步骤在数据库中进行更改。

1. 运行查询以查看中的前 10 个项**Warehouse.StockItems**表。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID"
   ```

   您应该看到的项标识符和名称的列表：

   ```
   StockItemID StockItemName
   ----------- -----------------
             1 USB missile launcher (Green)
             2 USB rocket launcher (Gray)
             3 Office cube periscope (Black)
             4 USB food flash drive - sushi roll
             5 USB food flash drive - hamburger
             6 USB food flash drive - hot dog
             7 USB food flash drive - pizza slice
             8 USB food flash drive - dim sum 10 drive variety pack
             9 USB food flash drive - banana
            10 USB food flash drive - chocolate bar
   ```

1. 使用以下更新的第一项的说明**更新**语句：

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName="USB missile launcher (Dark Green)" WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName='USB missile launcher (Dark Green)' WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   应看到类似于以下文本的输出：

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>创建新的备份

已将数据库还原到的容器之后，可能想要定期创建数据库备份正在运行的容器内。 步骤上一步骤，但按相反的顺序遵循类似的模式。

1. 使用**备份数据库**Transact-SQL 命令以在容器中创建的数据库备份。 本教程中创建一个新的备份文件， **wwi_2.bak**，在以前创建 **/var/opt/mssql/backup**目录。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   应看到类似于以下输出：

   ```
   10 percent processed.
   20 percent processed.
   30 percent processed.
   40 percent processed.
   50 percent processed.
   60 percent processed.
   70 percent processed.
   Processed 1200 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   80 percent processed.
   Processed 3865 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Processed 938 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   100 percent processed.
   BACKUP DATABASE successfully processed 59099 pages in 25.056 seconds (18.427 MB/sec).
   ```

1. 接下来，将复制出的容器和主机上的备份文件。

   ```bash
   cd ~
   sudo docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

   ```PowerShell
   cd ~
   docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

## <a name="use-the-persisted-data"></a>使用所保留的数据

除了保护您的数据执行数据库备份，还可以使用数据卷容器。 本教程中创建的开头**sql1**容器与`-v sql1data:/var/opt/mssql`参数。 **Sql1data**数据卷容器仍然存在 **/var/opt/mssql**数据即使在删除容器。 以下步骤中完全删除**sql1**容器，然后创建新的容器， **sql2**，使用所保留的数据。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 停止**sql1**容器。

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. 删除容器。 这不会删除以前创建**sql1data**数据卷容器并在它所保留的数据。

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 创建新的容器， **sql2**，并重用**sql1data**数据卷容器。

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

1. Wide World Importers 数据库现在位于新的容器。 运行一个查询，验证以前所做的更改。

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > SA 密码不是为指定的密码**sql2**容器， `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`。 所有 SQL Server 数据已从还原**sql1**，包括本教程前面从更改的密码。 实际上，由于还原 /var/opt/mssql 中的数据会忽略如下一些选项。 出于此原因，密码是`<YourNewStrong!Passw0rd>`如下所示。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 停止**sql1**容器。

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. 删除容器。 这不会删除以前创建**sql1data**数据卷容器并在它所保留的数据。

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 创建新的容器， **sql2**，并重用**sql1data**数据卷容器。

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
    ```

1. Wide World Importers 数据库现在位于新的容器。 运行一个查询，验证以前所做的更改。

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > SA 密码不是为指定的密码**sql2**容器， `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`。 所有 SQL Server 数据已从还原**sql1**，包括本教程前面从更改的密码。 实际上，由于还原 /var/opt/mssql 中的数据会忽略如下一些选项。 出于此原因，密码是`<YourNewStrong!Passw0rd>`如下所示。

::: moniker-end

## <a name="next-steps"></a>后续步骤

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

在本教程中，您学习了如何在 Windows 上备份数据库并将其移到运行 SQL Server 2017 的 Linux 服务器。 你将了解到：

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

在本教程中，您学习了如何在 Windows 上备份数据库并将其移到运行 SQL Server 2019 预览版的 Linux 服务器。 你将了解到：

::: moniker-end

> [!div class="checklist"]
> * 创建 SQL Server Linux 容器映像。
> * 将 SQL Server 数据库备份复制到容器中。
> * 运行与在容器内的 TRANSACT-SQL 语句**sqlcmd**。
> * 创建和提取在容器中的备份文件。
> * 使用在 Docker 中的数据卷容器将 SQL Server 数据持久保存。

接下来，查看其他 Docker 配置和故障排除方案：

> [!div class="nextstepaction"]
>[SQL Server 2017 的 Docker 配置指南](sql-server-linux-configure-docker.md)
