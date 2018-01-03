---
title: "已更新-Linux 文档上的 SQL Server |Microsoft 文档"
description: "显示有关最近更改中的文档，在 Linux 上的 Microsoft SQL server 的更新内容的代码段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: rothja
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: linux-sql
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: 030f30580b0ddb02da2a67990d0c58acf15236c9
ms.sourcegitcommit: 73043fe1ac5d60b67e33b44053c0a7733b98bc3d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2017
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>新的和最近的更新： Linux 文档上的 SQL Server



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：从 2017-09-28 到 2017-12-02&nbsp;&nbsp;&nbsp;
- *主题区域：* &nbsp; **在 Linux 上的 Microsoft SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [在云中运行 SQL Server 2017](quickstart-install-connect-clouds.md)
2. [从预览版存储库的存储库更改到 GA 存储库](sql-server-linux-change-repo.md)
3. [性能最佳实践和 SQL Server 自 2017 年在 Linux 上的配置指南](sql-server-linux-performance-best-practices.md)
4. [故障转移群集实例-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-concepts.md)
5. [配置故障转移群集实例-iSCSI-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
6. [配置 NFS-在 Linux 上的 SQL Server 的故障转移群集实例-](sql-server-linux-shared-disk-cluster-configure-nfs.md)
7. [配置 SMB-在 Linux 上的 SQL Server 的故障转移群集实例-](sql-server-linux-shared-disk-cluster-configure-smb.md)
8. [运行故障转移群集实例-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-operate.md)
9. [限制和 Linux 上的 SSIS 的已知的问题](sql-server-linux-ssis-known-issues.md)
10. [还原 Linux Docker 容器中的 SQL Server 数据库](tutorial-restore-backup-in-sql-server-container.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [使用 Docker 运行 SQL Server 2017 容器映像](#TitleNum_1)
2. [为在 Linux 上的 SQL Server 中配置 Alwayson 可用性组](#TitleNum_2)
3. [可用性组配置的高可用性和数据保护](#TitleNum_3)
4. [在 Docker 上配置 SQL Server 2017 容器映像](#TitleNum_4)
5. [加密连接到 Linux 上的 SQL Server](#TitleNum_5)
6. [创建和运行在 Linux 上的 SQL Server 代理作业](#TitleNum_6)
7. [在 Linux 上的 SQL Server 安装指南](#TitleNum_7)
8. [配置故障转移群集实例的 SQL Server 上 Linux (RHEL)](#TitleNum_8)
9. [解决在 Linux 上的 SQL Server](#TitleNum_9)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-run-the-sql-server-2017-container-image-with-dockerquickstart-install-connect-dockermd"></a>1.&nbsp;[使用 Docker 运行 SQL Server 2017 容器映像](quickstart-install-connect-docker.md)

更新日期：2017-11-30 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[下一篇](#TitleNum_2)）

<!-- Source markdown line 261.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2aaf953c2f1fb675b1304186108fbef1eebf6f8f f7cd42bb320a8892a5ec63ce999186438097636a  (PR=4150  ,  Filename=quickstart-install-connect-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



**删除容器**


如果你想要删除 SQL Server 容器使用在本教程中，运行以下命令：

```
sudo docker stop sql1
sudo docker rm sql1
```

```
docker stop sql1
docker rm sql1
```

> [!WARNING]
> 停止并永久删除容器中删除容器中的任何 SQL Server 数据。 如果你需要以保留数据，[创建和复制将备份文件签出 container--tutorial-restore-backup-in-sql-server-container.md） 或使用 [容器数据暂留 technique--sql-server-linux-configure-docker.md#persist）。




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-always-on-availability-group-for-sql-server-on-linuxsql-server-linux-availability-group-configure-hamd"></a>2.&nbsp;[配置 Alwayson 可用性组在 Linux 上的 SQL server](sql-server-linux-availability-group-configure-ha.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 129.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3c7e6bc862e5b062a855918efbeee5fe748b7236 6900c9a30ce04ce54e7aaa270ef7d276c18f9afd  (PR=4150  ,  Filename=sql-server-linux-availability-group-configure-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



- 创建具有两个同步副本和配置副本的可用性组：

   >[!IMPORTANT]
   >此体系结构允许任何版本的 SQL Server 以承载第三个副本。 例如，可以在 SQL Server Enterprise Edition 上承载的第三个副本。 在 Enterprise Edition 上是唯一有效的终结点类型`WITNESS`。

```sql
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
       N'**<node1>**' WITH (
          ENDPOINT_URL = N'tcp://**<node1>**:**<5022>**',
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
          FAILOVER_MODE = EXTERNAL,
          SEEDING_MODE = AUTOMATIC
          ),
       N'**<node2>**' WITH (
          ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**',
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
          FAILOVER_MODE = EXTERNAL,
          SEEDING_MODE = AUTOMATIC
          ),
       N'**<node3>**' WITH (
          ENDPOINT_URL = N'tcp://**<node3>**:**<5022>**',
          AVAILABILITY_MODE = CONFIGURATION_ONLY
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-high-availability-and-data-protection-for-availability-group-configurationssql-server-linux-availability-group-hamd"></a>3.&nbsp;[可用性组配置的高可用性和数据保护](sql-server-linux-availability-group-ha.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 106.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e6bee794ce19f1ed62298b4a0cce7207550f1595 b64726cd6e91721850721786d26c170d59fc320a  (PR=4150  ,  Filename=sql-server-linux-availability-group-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



默认值为`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`为 0。 下表描述可用性行为。

| |高可用性 （& a) </br> 数据保护 | 数据保护
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|@shouldalert
|主要副本中断 | 自动故障转移。 新的主是 R / 瓦 | 自动故障转移。 新的主数据库不可用的用户事务。
|辅助副本中断 | 主数据库处于 R/W，运行已公开到数据丢失 （如果主失败并且无法恢复）。 如果主没有自动故障转移也会失败。 | 主也无法供用户事务。 如果主故障转移到没有副本也会失败。
|配置仅副本中断 | 主是 R / 瓦 如果主没有自动故障转移也会失败。 | 主是 R / 瓦 如果主没有自动故障转移也会失败。
|同步辅助 + 配置仅副本中断| 主也无法供用户事务。 自动故障转移。 | 主也无法供用户事务。 故障转移到如果没有副本以及主服务器失败。
<sup>*</sup>默认值

>[!NOTE]
>承载配置唯一的副本的 SQL Server 的实例还可以托管其他数据库。 此外可以参与作为多个可用性组的配置数据库。

**要求**


* 可用性组中的配置仅副本的所有副本都必须都是 SQL Server 自 2017 年 CU 1 或更高版本。
* 任何版本的 SQL Server 可以承载配置仅副本，包括 SQL Server Express。
* 可用性组都需要至少一个辅助副本-除了主副本。
* 配置仅副本不会计入每个 SQL Server 实例的副本最大数目。 SQL Server 标准版允许最多三个副本，SQL Server 企业版则允许最多 9。



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-configure-sql-server-2017-container-images-on-dockersql-server-linux-configure-dockermd"></a>4.&nbsp;[Docker 上的配置 SQL Server 2017 容器映像](sql-server-linux-configure-docker.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_3) | [下一步](#TitleNum_5))

<!-- Source markdown line 34.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c759fb88ae8d654414202f28c5fc58dfd02581bf fd270118f2f4608fceaf563fc143951b41097bdb  (PR=4150  ,  Filename=sql-server-linux-configure-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



此配置主题提供了下面的部分中的其他使用方案。

**<a id="production"></a>运行容器映像的生产**


上一节中的快速入门从 Docker Hub 中运行 SQL Server 的免费的开发人员版。 如果你想要运行容器映像，例如 Enterprise、 Standard、 或 Web edition 的生产，仍将应用的大部分信息。 但是，有一些区别此处所述。

- 如果你具有有效的许可证，你只可以在生产环境中使用 SQL Server。 你可以获取免费的 SQL Server Express 生产许可证[此处](https://go.microsoft.com/fwlink/?linkid=857693)。 SQL Server Standard 和 Enterprise Edition 许可证均可通过[Microsoft 批量许可](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs.aspx)。

- 必须从请求生产 SQL Server 容器映像[Docker 存储](https://store.docker.com)。 如果你还没有一个 Docker 存储上创建帐户。

- 开发人员容器映像 Docker 存储上的可以配置为运行的生产版本。 使用以下步骤运行生产版本：

   1. 首先，登录到你的 docker id 从命令行。

```
      docker login
```

   1. 接下来，你需要获取免费的开发人员 Docker 存储上的容器映像。 转到[https://store.docker.com/images/mssql-server-linux](https://store.docker.com/images/mssql-server-linux)，单击**结帐**，并按照说明操作。

   1. 检查要求，然后运行过程中与 [快速入门-快速入门-安装-连接-docker.md）。 但有两个的差异。 你必须拉取映像**存储/microsoft/mssql-服务器-linux:\<标记名称\>** Docker 存储区中。 并且你必须指定与生产版本**MSSQL_PID**环境变量。 下面的示例演示如何为 Enterprise Edition 运行最新的 SQL Server 2017 容器映像：



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-encrypting-connections-to-sql-server-on-linuxsql-server-linux-encrypted-connectionsmd"></a>5.&nbsp;[加密到 Linux 上的 SQL Server 的连接](sql-server-linux-encrypted-connections.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_4) | [下一步](#TitleNum_6))

<!-- Source markdown line 45.  ms.author= meetb;rickbyh.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7e3187866df060903e30000d60d673edad46d210 bcb1f2771e6c29b535a30b9f23ac296954509187  (PR=4150  ,  Filename=sql-server-linux-encrypted-connections.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



        sudo chown mssql:mssql mssql.pem mssql.key
        sudo chmod 600 mssql.pem mssql.key
        sudo mv mssql.pem /etc/ssl/certs/
        sudo mv mssql.key /etc/ssl/private/

- **将 SQL Server 配置**

        systemctl stop mssql-server
        cat /var/opt/mssql/mssql.conf
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0

- **注册客户端计算机 （Windows、 Linux 或 macOS） 上的证书**

    -   如果您正在使用需要复制到客户端计算机上而不是用户证书的证书颁发机构 (CA) 证书的 CA 签名的证书。
    -   如果你只需使用的自签名的证书的.pem 文件复制到分发到相应的以下文件夹并执行命令以启用它们

        - **Windows**： 导入为下当前用户证书的.pem 文件-> 受信任根证书颁发机构证书->
        - **macOS**:

-   **连接字符串示例**

    - **..!包括 NotShown-ssmanstudiofull md.../includes/ssmanstudiofull-md.md)]** ！ [SSMS 连接 dialog--media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png"SSMS 连接对话框"）



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-create-and-run-sql-server-agent-jobs-on-linuxsql-server-linux-run-sql-server-agent-jobmd"></a>6.&nbsp;[创建和运行在 Linux 上的 SQL Server 代理作业](sql-server-linux-run-sql-server-agent-job.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_5) | [下一步](#TitleNum_7))

<!-- Source markdown line 35.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1598129bb5f98434435d8ad02336a9adf76c7870 6fe3fe7df3a60dbac31f1df59aac9860d293421a  (PR=4150  ,  Filename=sql-server-linux-run-sql-server-agent-job.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



完成本教程所需的以下先决条件：

* Linux 计算机满足以下先决条件：
  * SQL Server 2017 ([RHEL--quickstart-install-connect-red-hat.md)，[SLES-快速入门-安装-连接-suse.md)，或 [Ubuntu-快速入门-安装-连接-ubuntu.md)) 使用命令行工具。

以下先决条件是可选的：

* 使用 SSMS 的 Windows 计算机：
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)有关可选 SSMS 步骤。

**安装 SQL Server 代理**


若要在 Linux 上使用 SQL Server 代理，必须首先安装**mssql server 代理**已安装的 SQL Server 2017 的计算机上的包。

1. 安装**mssql server 代理**使用适合于您的 Linux 操作系统的命令。

   | 平台 | 安装命令 |
   |-----|-----|
   | RHEL | `sudo yum install mssql-server-agent` |
   | SLES | `sudo zypper refresh`<br/>`sudo zypper update mssql-server-agent` |
   | Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server-agent` |

1. 使用以下命令重新启动 SQL Server:

```
   sudo systemctl restart mssql-server
```

**创建示例数据库**


使用以下步骤创建一个名为的示例数据库**SampleDB**。 此数据库用于日常备份作业。

1. 在 Linux 计算机上打开 bash 终端会话。



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-installation-guidance-for-sql-server-on-linuxsql-server-linux-setupmd"></a>7.&nbsp;[在 Linux 上的 SQL Server 安装指南](sql-server-linux-setup.md)

*更新时间： 自 2017 年 1-12-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_6) | [下一步](#TitleNum_8))

<!-- Source markdown line 125.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 8ba2bf6f9cf4b5f54a6ee0f4d16d4437d5724880 eedddcfb64c6432215f56b74dc91700d9804fce8  (PR=4160  ,  Filename=sql-server-linux-setup.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=085dd05d56afecbb454206ed8402cfbaa597cfbe) -->



**<a id="repositories"></a>配置源存储库**


当安装或升级 SQL Server 时，你从你配置的 Microsoft 存储库中获取最新版本的 SQL Server。

**存储库选项**


有两种主要类型的每个分布的存储库：

- **累积更新 (CU)**: 累积更新 (CU) 存储库包含自该版本为基的 SQL Server 版本和任何 bug 修复或改进的包。 累积更新是特定于发行版中，如 SQL Server 自 2017 年。 正则的频率发布它们。

- **GDR**: GDR 储存库自该版本中包含的基本 SQL Server 版本和仅关键的修复程序和安全更新的包。 这些更新也会添加到下一步 CU 发行版。

每个 CU 和 GDR 版本包含完整的 SQL Server 程序包和所有以前的更新，该存储库。 从 GDR 版本更新到 CU 版本受更改 SQL Server 配置的存储库。 你还可以 [降级-#rollback） 到在主要版本中的任何版本 (ex： 自 2017 年)。 更新从 CU 的 GDR 发行版的版本不支持。

**检查你配置的存储库**


如果你想要验证配置了哪些存储库，使用以下依赖于平台的方法。

| 平台 | 过程 |
|-----|-----|
| RHEL | 1.查看中的文件**/etc/yum.repos.d**目录：`sudo ls /etc/yum.repos.d`<br/>2.查找配置 SQL Server 目录中，如文件**mssql server.repo**。<br/>3.输出文件的内容：`sudo cat /etc/yum.repos.d/mssql-server.repo`<br/>4.**名称**属性是配置的存储库。|
| SLES | 1.运行以下命令：`sudo zypper info mssql-server`<br/>2.**存储库**属性是配置的存储库。 |
| Ubuntu | 1.运行以下命令：`sudo cat /etc/apt/sources.list`<br/>2.检查 mssql 服务器的程序包 URL。 |



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-configure-failover-cluster-instance---sql-server-on-linux-rhelsql-server-linux-shared-disk-cluster-configuremd"></a>8.&nbsp;[配置故障转移群集实例的 SQL Server 上 Linux (RHEL)](sql-server-linux-shared-disk-cluster-configure.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_7) | [下一步](#TitleNum_9))

<!-- Source markdown line 25.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 308fa1809c80a009f7f15b5ca6917f6b76588c3e 71f18baa320041ff10c94e8c7668e40dff45cac3  (PR=4150  ,  Filename=sql-server-linux-shared-disk-cluster-configure.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



> [!div class="checklist"]
> * 设置和配置 Linux
> * 安装和配置 SQL Server
> * 配置主机文件
> * 配置共享的存储并移动数据库文件
> * 在每个群集节点上安装和配置 Pacemaker
> * 配置故障转移群集实例

此文章介绍了如何为 SQL Server 中创建两个节点共享的磁盘故障转移群集实例 (FCI)。 本文章包括说明和脚本示例的 Red Hat Enterprise Linux (RHEL)。 Ubuntu 分发是类似于 RHEL，因此脚本示例将通常还在 Ubuntu 上工作。

概念信息，请参阅 [SQL Server 故障转移群集实例 (FCI) 上 Linux--sql-server-linux-shared-disk-cluster-concepts.md)。

**先决条件**


若要完成以下端到端方案需要两台计算机部署两个节点群集和另一个服务器作为存储。 以下步骤概述了如何配置这些服务器。

**设置和配置 Linux**


第一步是在群集节点上配置操作系统。 在群集中的每个节点上配置 linux 分发。 在这两个节点上使用相同的分发和版本。 使用一个或多个以下的分发：

* RHEL HA 外接程序的有效订阅

**安装和配置 SQL Server**


1. 在这两个节点上设置 SQL Server 和安装。  有关详细说明，请参阅 [安装 SQL Server 上 Linux-sql server-linux setup.md)。
1. 出于配置目的，请将一个节点指定为主要节点，而将另一个指定为辅助节点。 使用以下术语，按照此指南操作。
1. 在辅助节点上，停止并禁用 SQL Server。
    以下示例将停止并禁用 SQL Server：
```
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
```

    > [!NOTE]
    > At set up time, a Server Master Key is generated for the SQL Server instance and placed at `var/opt/mssql/secrets/machine-key`. On Linux, SQL Server always runs as a local account called mssql. Because it's a local account, its identity isn't shared across nodes. Therefore, you need to copy the encryption key from primary node to each secondary node so each local mssql account can access it to decrypt the Server Master Key.



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-troubleshoot-sql-server-on-linuxsql-server-linux-troubleshooting-guidemd"></a>9.&nbsp;[解决在 Linux 上的 SQL Server](sql-server-linux-troubleshooting-guide.md)

更新日期：2017-11-30 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_8)）

<!-- Source markdown line 125.  ms.author= anshrest.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5f8557a34b38e028ff6e5ac370b6d2d6bf315091 196e56187b57bdd79cc5cdc5e6fce3d41e82af0c  (PR=4150  ,  Filename=sql-server-linux-troubleshooting-guide.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



**在最小配置中或在单用户模式下启动 SQL Server**


**在最小配置模式下启动 SQL Server**

在配置值的设置（例如，过度分配内存）妨碍服务器启动时，这非常有用。

```
   sudo -u mssql /opt/mssql/bin/sqlservr -f
```

**在单用户模式下启动 SQL Server**

在某些情况下，你可能需要使用启动选项-m 在单用户模式下启动 SQL Server 的实例。 例如，您可能要更改服务器配置选项或恢复已破坏的 master 数据库或其他系统数据库。 例如，你可能想要更改服务器配置选项或恢复已损坏的主数据库或其他系统数据库

在单用户模式下启动 SQL Server
```
   sudo -u mssql /opt/mssql/bin/sqlservr -m
```

在使用 SQLCMD 单用户模式下启动 SQL Server
```
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
```

> [!WARNING]
>  使用“mssql”用户启动 Linux 上的 SQL Server 以防止将来的启动问题。 例如，“sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]”

如果你意外已经与另一个用户启动 SQL Server，你将需要改回为之前从 SQL Server 开始 systemd mssql 用户的 SQL Server 数据库文件的所有权。 例如，若要将 /var/opt/mssql 下的所有数据库文件的所有权更改为 mssql 的用户，请运行以下命令

```
   chown -R mssql:mssql /var/opt/mssql/
```







## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新文章和更新的文章 (3+14)：SQL 高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新的和更新的文章 (1+0)：Analysis Services for SQL 文档](../analysis-services/new-updated-analysis-services.md)
- [新文章和更新的文章 (87+0)：SQL 分析平台系统文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章和更新的文章 (5+4)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新文章和更新的文章 (0+1)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新文章和更新的文章 (2+2)：SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)
- [新文章和更新的文章 (10+9)：Linux 版 SQL 文档](../linux/new-updated-linux.md)
- [新文章和更新的文章 (2+4)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新文章和更新的文章 (4+2)：SQL Reporting Services 文档](../reporting-services/new-updated-reporting-services.md)
- [新文章和更新的文章 (0+1)：SQL 示例文档](../sample/new-updated-sample.md)
- [新文章和更新的文章 (21+0)：SQL Operations Studio 文档](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章和更新的文章 (5+1)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新的和更新的文章 (0+1)：SQL Server Data Tool (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新文章和更新的文章 (1+0)：SQL Server 迁移助手 (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新的和更新的文章 (0+1)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新文章和更新的文章 (0+2)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新文章和更新的文章 (0+0)：SQL 数据迁移助手 (DMA) 文档](../dma/new-updated-dma.md)
- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新文章和更新的文章 (0+0)：SQL 工具文档](../tools/new-updated-tools.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)


