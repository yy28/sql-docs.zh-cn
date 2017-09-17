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
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 9e6b139e45ccb5184255eabedfb0f809ff64fd2b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>新的和最近的更新： Linux 文档上的 SQL Server



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- *日期范围的更新：* &nbsp; **自 2017 年 1-07-18** &nbsp;到&nbsp;**自 2017 年 1-09-11**
- *主题区域：* &nbsp; **在 Linux 上的 Microsoft SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

以下链接跳转到最近已添加的新项目。


1. [数据库邮件和 Linux 上的 SQL 代理的电子邮件警报](sql-server-linux-db-mail-sql-agent.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分显示的摘自从最近出现了大规模更新的文章中收集的更新。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此 compact 列表提供了有关摘录部分中列出的所有更新的文章的链接。

1. [运行的 Linux 上的 SQL Server 的 HA 可用性组](#TitleNum_1)
2. [在 Docker 上配置 SQL Server 2017 容器映像](#TitleNum_2)
3. [使用 mssql conf 工具在 Linux 上配置 SQL Server](#TitleNum_3)
4. [在 Linux 上的 SQL Server 的客户反馈](#TitleNum_4)
5. [从 Windows 的 SQL Server 数据库迁移到使用备份和还原的 Linux](#TitleNum_5)
6. [在 Linux 上的 SQL Server 2017 的发行说明](#TitleNum_6)
7. [在 Linux 上的 SQL Server 安装指南](#TitleNum_7)
8. [在 Linux 上安装 SQL Server Integration Services (SSIS)](#TitleNum_8)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-operate-ha-availability-group-for-sql-server-on-linuxsql-server-linux-availability-group-failover-hamd"></a>1.&nbsp;[运行 HA 可用性组在 Linux 上的 SQL Server](sql-server-linux-availability-group-failover-ha.md)

*更新时间： 自 2017 年-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 167.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1bef3ece125721b041aa2b9d836329736377df8d 669d2b9a614d680b98280d5b522ba82cf466536c  (PR=2948  ,  Filename=sql-server-linux-availability-group-failover-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



**升级的可用性组**


在升级某一可用性组之前，审阅的最佳实践在 [升级可用性组副本实例.../ database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md）。

以下各节说明如何使用可用性组在 Linux 上执行滚动升级 SQL Server 实例。

**在 Linux 上的升级步骤**


在 Linux 中的 SQL Server 实例上可用性组副本时，可用性组的群集类型是`EXTERNAL`或`NONE`。 除了 Windows Server 故障转移群集 (WSFC) 是之外，由群集管理器管理的可用性组`EXTERNAL`。 Pacemaker 使用 Corosync 是外部的群集管理器的示例。 具有未群集管理器的可用性组具有群集类型`NONE`此处所述的升级步骤是特定于可用性组的群集类型`EXTERNAL`或`NONE`。

1. 在开始之前，备份每个数据库。
2. 升级该主机辅助副本的 SQL Server 实例。

    a. 首先升级异步辅助副本。

    b. 升级同步辅助副本。

   >[!NOTE]
   >如果某一可用性组仅有异步副本-为了避免丢失任何数据更改为同步的一个副本，并等待，直到它已同步。 然后升级此副本。

   b.1。 在承载辅助副本针对升级的节点上停止资源

   在运行升级命令之前停止资源，以便群集将不监视它并不必要地将其故障。 下面的示例添加要停止对资源将导致的节点上的位置约束。 更新`ag_cluster-master`在资源名称和`nodeName1`与承载副本针对升级的节点。

```
   pcs constraint location ag_cluster-master avoids nodeName1
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-sql-server-2017-container-images-on-dockersql-server-linux-configure-dockermd"></a>2.&nbsp;[Docker 上的配置 SQL Server 2017 容器映像](sql-server-linux-configure-docker.md)

*更新时间： 2017年-09-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 257.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0239ed55a23721eedcc0407a0886d08da47c975b 108fe230151cff7dc91fcdc22218f232394746ec  (PR=3050  ,  Filename=sql-server-linux-configure-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=60272ce672c0a32738b0084ea86f8907ec7fc0a5) -->



1. 标识 Docker**标记**你想要使用的版本。 若要查看可用的标记，请参阅[mssql server linux Docker 中心页](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/)。

1. 请求具有标记的 SQL Server 容器映像。 例如，若要请求 RC1 映像，请替换`<image_tag>`在下面的命令与`rc1`。

```
   docker pull microsoft/mssql-server-linux:<image_tag>
```

1. 若要使用该映像运行新的容器，指定中的标记名称`docker run`命令。 在以下命令，将`<image_tag>`与你想要运行的版本。

```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

这些步骤还可以用于降级现有容器。 例如，你可能希望回滚或降级进行疑难解答或测试正在运行的容器。 若要降级正在运行的容器，你必须使用持久性技术数据文件夹。 遵循相同的步骤中所述 [升级部分-#upgrade），但运行新容器时指定的较旧版本的标记名称。

> [!IMPORTANT]



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-configure-sql-server-on-linux-with-the-mssql-conf-toolsql-server-linux-configure-mssql-confmd"></a>3.&nbsp;[使用 mssql conf 工具的 Linux 上配置 SQL Server](sql-server-linux-configure-mssql-conf.md)

*更新时间： 2017年-09-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 233.  ms.author= lbosq.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6117f03e9617b70077488d86f94b32537c4cb9e8 4247a749c056037dd71a27121525be04be6a4f21  (PR=3042  ,  Filename=sql-server-linux-configure-mssql-conf.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=46b16dcf147dbd863eec0330e87511b4ced6c4ce) -->



**<a id="localaudit"></a>设置本地审核目录**


**Telemetry.userrequestedlocalauditdirectory**设置启用本地审核和创建的允许你设置目录，其中本地的审核日志。

1. 创建新的本地审核日志的目标目录。 下面的示例创建一个新**/tmp/审核**目录：

```
   sudo mkdir /tmp/audit
```

1. 更改所有者和到的目录组**mssql**用户：

```
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
```

1. Mssql conf 脚本作为根与运行**设置**命令**telemetry.userrequestedlocalauditdirectory**:

```
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
```

1. 重新启动 SQL Server 服务：

```
   sudo systemctl restart mssql-server
```

有关详细信息，请参阅 [Linux--sql-server-linux-customer-feedback.md 上的 SQL Server 客户的反馈。）

**<a id="lcid"></a>更改 SQL Server 区域设置**


**Language.lcid**将更改的 SQL Server 区域设置设置为任何受支持的语言标识符 (LCID)。

1. 下面的示例更改为法语的区域设置 (1036):

```
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
```

1. 重新启动 SQL Server 服务以应用所做的更改：

```
   sudo systemctl restart mssql-server
```

**<a id="memorylimit"></a>设置内存限制**


**Memory.memorylimitmb**将控件设置为 SQL Server 的物理内存量 （以 mb 为单位） 可用。 默认值为 80%的物理内存。

1. Mssql conf 脚本作为根与运行**设置**命令**memory.memorylimitmb**。 下面的示例更改为 SQL Server 到 3.25 GB (3328 MB) 的可用内存。

```
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
```

1. 重新启动 SQL Server 服务以应用所做的更改：



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-customer-feedback-for-sql-server-on-linuxsql-server-linux-customer-feedbackmd"></a>4.&nbsp;[在 Linux 上的 SQL Server 的客户反馈](sql-server-linux-customer-feedback.md)

*更新时间： 自 2017 年-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_3) | [下一步](#TitleNum_5))

<!-- Source markdown line 104.  ms.author= anshrest.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9d8122e864804004d91f6b7c5c3d24c4a4114d34 7316ef831c390a854c324f23a02c3fb6005e2fea  (PR=2948  ,  Filename=sql-server-linux-customer-feedback.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->




**在 Docker 上**

若要在 docker 上启用本地审核必须 Docker [保留你 data--sql-server-linux-configure-docker.md）。

1. 新的本地审核日志的目标目录将容器中。 在您的计算机上的主机目录中创建新的本地审核日志的目标目录。 下面的示例创建一个新**/审核**目录：

```
   sudo mkdir <host directory>/audit
```


1. 添加`mssql.conf`文件替换为行`[telemetry]`和`userrequestedlocalauditdirectory = <host directory>/audit`主机目录中：

```
   echo '[telemetry]' >> <host directory>/mssql.conf
```

```
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
```
2. 运行容器映像
```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

**后续步骤**





&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restoresql-server-linux-migrate-restore-databasemd"></a>5.&nbsp;[从 Windows 的 SQL Server 数据库迁移到使用备份和还原的 Linux](sql-server-linux-migrate-restore-database.md)

*更新时间： 自 2017 年-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_4) | [下一步](#TitleNum_6))

<!-- Source markdown line 30.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e78f5516a46eab834f644979d3e1c0ca415fabcd 6b03a01385078290b9f451ac013b628f53e0e8b4  (PR=2948  ,  Filename=sql-server-linux-migrate-restore-database.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



* 替换为以下的 Windows 计算机：
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions)安装。
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)安装。
  * 要迁移的目标数据库。

* 具有安装以下版本的 Linux 计算机：
  * SQL Server 自 2017 年 1 RC2。 请参阅的安装快速入门 [RHEL--quickstart-install-connect-red-hat.md)，[SLES-快速入门-安装-连接-suse.md)，或 [Ubuntu-快速入门-安装-连接-ubuntu.md)。
  * SQL Server 自 2017 年 1 RC2 [命令行 tools--sql-server-linux-setup-tools.md)。

**在 Windows 上创建备份**


有多种方法可以在 Windows 上创建数据库的备份文件。 以下步骤使用 SQL Server Management Studio (SSMS)。

1. 启动**SQL Server Management Studio** Windows 计算机上。

1. 在连接对话框中，输入**localhost**。

1. 在对象资源管理器，展开**数据库**。



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>6.&nbsp;[有关在 Linux 上的 SQL Server 2017 发行说明](sql-server-linux-release-notes.md)

*更新时间： 自 2017 年-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_5) | [下一步](#TitleNum_7))

<!-- Source markdown line 31.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 4c8b9876f4792782314ba2f9b246405fb8036f84 acb97cf0a2e0bdd039575eaab9c41003316cbb02  (PR=2939  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



**<a id="RC2"></a>RC2 (自 2017 年 8 月)**


对于此版本的 SQL Server 引擎版本是 14.0.900.75。

**支持的平台**


| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 工作站、 服务器和桌面 | XFS 或 EXT4 | [安装 guide--quickstart-install-connect-red-hat.md) |
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [安装指南-快速入门-安装-连接-suse.md） |
| Ubuntu 16.04LTS | EXT4 | [安装指南-快速入门-安装-连接-ubuntu.md） |
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | N/A | [安装指南-快速入门-安装-连接-docker.md） |

> [!NOTE]
> 至少需要 3.25GB 内存才能在 Linux 上运行 SQL Server。
> SQL Server 引擎已在此时间测试 1.5 TB 的内存。

**包的详细信息**


下表列出了包的详细信息以及 RPM 和 Debian 包的下载位置。 请注意，如果使用以下安装指南中的步骤，则无需直接下载这些包：

- [安装 SQL Server 程序包-sql server-linux setup.md）
- [安装全文搜索 package--sql-server-linux-setup-full-text-search.md）
- [安装 SQL Server 代理 package--sql-server-linux-setup-sql-agent.md）

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.900.75-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) |



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-installation-guidance-for-sql-server-on-linuxsql-server-linux-setupmd"></a>7.&nbsp;[在 Linux 上的 SQL Server 安装指南](sql-server-linux-setup.md)

*更新时间： 自 2017 年-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_6) | [下一步](#TitleNum_8))

<!-- Source markdown line 70.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 00394e1733568a55243788d828968ff9b58a3c99 8ba2bf6f9cf4b5f54a6ee0f4d16d4437d5724880  (PR=2971  ,  Filename=sql-server-linux-setup.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=303d3b74da3fe370d19b7602c0e11e67b63191e7) -->



**<a id="rollback"></a>回滚 SQL Server**


回滚或降级到以前的版本的 SQL Server，使用以下步骤：

1. 标识你想要降级到 SQL Server 程序包的版本号。 有关包号码的列表，请参阅 [版本 notes--sql-server-linux-release-notes.md。)

1. 降级到以前的版本的 SQL Server。 在以下命令，将`<version_number>`与您在第一步中标识的 SQL Server 版本号。

   | 平台 | 包更新命令 |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> 它仅支持降级的相同的主版本，如 SQL Server 自 2017 年中的发行版。

> [!IMPORTANT]
> 仅支持 RC2 和 RC1 之间此时进行降级。




&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-install-sql-server-integration-services-ssis-on-linuxsql-server-linux-setup-ssismd"></a>8.&nbsp;[在 Linux 上安装 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)

*更新时间： 自 2017 年-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_7))

<!-- Source markdown line 66.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a3fecd2553d1b25406445b8a26b22c9015dd98fe f836d560513fef1217e7dbce0ab85f78eec6f937  (PR=2948  ,  Filename=sql-server-linux-setup-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



如果你已有`mssql-server-is`安装，你可以更新到最新版本使用以下命令：

```
sudo apt-get install mssql-server-is
```


若要删除`mssql-server-is`，可以运行以下命令：
```
sudo apt-get remove msssql-server-is
```



**<a name="RHEL"></a>在 RHEL 上安装 SSIS**

若要安装`mssql-server-is`打包在 RHEL 上，执行以下步骤：


1.  进入超级用户模式。

```
    sudo su
```


2.  下载 Microsoft SQL Server Red Hat 存储库配置文件。

```
    curl https://packages.microsoft.com/config/rhel/7/mssql-server.repo > /etc/yum.repos.d/mssql-server.repo
```


3.  退出超级用户模式。

```
    exit
```


4.  运行以下命令以安装 SQL Server Integration Services。

```
    sudo yum install -y mssql-server-is
```


5.  安装完成后，请运行`ssis-conf`。







## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本部分列出了一些非常类似文章中我们公共 GitHub.com 存储库中的其他主题区域的最近更新项目： [MicrosoftDocs/sql 文档](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新 + 更新 (3 + 12): **sql 高级分析**文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (5 + 0):**连接到 SQL**文档](../connect/new-updated-connect.md)
- [新 + 更新 (5 + 1): **sql 数据库引擎**文档](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (19 + 82): **sql Integration Services**文档](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (1 + 8): **sql Linux**文档](../linux/new-updated-linux.md)
- [新 + 更新 (12 + 1): **sql 的关系数据库**文档](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (0 + 1): **sql Reporting Services**文档](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (7 + 1): **Microsoft SQL Server**文档](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (1 + 1): **SQL Server Data Tools (SSDT)**文档](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (0 + 2): **SQL Server 迁移助手 (SSMA)**文档](../ssma/new-updated-ssma.md)
- [新 + 更新 (1 + 4): **SQL Server Management Studio (SSMS)**文档](../ssms/new-updated-ssms.md)
- [新 + 更新 (4 + 1): **TRANSACT-SQL**文档](../t-sql/new-updated-t-sql.md)
- [新 + 更新 (0 + 1): **SQL 的工具**文档](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新 + 更新 (0 + 0): **Analysis Services for SQL**文档](../analysis-services/new-updated-analysis-services.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新 + 更新 (0 + 0): **sql 的 Master Data Services (MDS)**文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../sample/new-updated-sample.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)



