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
ms.date: 07/17/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 13c237af359c543f6a99a0fce101af81b5eb2bcf
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>新的和最近的更新： Linux 文档上的 SQL Server

几乎每日 Microsoft 及其现有的文章的一些上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文档网站。 这篇文章显示摘录最近已更新的文章。 可能还会列出链接到新的文章。

定期重新运行程序生成这篇文章。 有时摘录可使用不完善格式，或出现 markdown 源文章中的说明。 此处永远不会显示图像。

报告的以下日期范围和主题的新的更新：



- *日期范围的更新：* &nbsp; **自 2017 年 1-05-23** &nbsp;到&nbsp;**自 2017 年 1-07-17**
- *主题区域：* &nbsp; **在 Linux 上的 Microsoft SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新项目

单击以下链接可跳转到最近添加的新文章。


1. [使用 Docker 运行 SQL Server 2017 容器映像](quickstart-install-connect-docker.md)
2. [安装 SQL Server 和 Red Hat 上创建数据库](quickstart-install-connect-red-hat.md)
3. [安装 SQL Server 和 SUSE Linux Enterprise Server 上创建数据库](quickstart-install-connect-suse.md)
4. [安装 SQL Server，并在 Ubuntu 上创建数据库](quickstart-install-connect-ubuntu.md)
5. [示例： 无人参与的 SQL Server 安装脚本以 Red Hat Enterprise Linux](sample-unattended-install-redhat.md)
6. [适用于 SUSE Linux Enterprise Server 的示例： 无人参与的 SQL Server 安装脚本](sample-unattended-install-suse.md)
7. [示例： 适用于 Ubuntu 的无人参与的 SQL Server 安装脚本](sample-unattended-install-ubuntu.md)
8. [在 Linux 上的 SQL 服务器的 active Directory 身份验证](sql-server-linux-active-directory-authentication.md)
9. [可用性组配置的高可用性和数据保护](sql-server-linux-availability-group-ha.md)
10. [在 Docker 上配置 SQL Server 2017 容器映像](sql-server-linux-configure-docker.md)
11. [在 Linux 上的 SQL Server 的客户反馈](sql-server-linux-customer-feedback.md)
12. [加密连接到 Linux 上的 SQL Server](sql-server-linux-encrypted-connections.md)
13. [在 Linux 上安装 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)




&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact 的最近更新的文章的列表

此 compact 列表提供了将在摘要部分中列出的所有更新文章的链接。



&nbsp;

## <a name="updated-articles-with-excerpts"></a>与摘录更新的文章

此部分显示的摘自从最近出现了大规模更新的文章中收集的更新。

此处显示的摘自其正确的语义上下文的来自分隔。 此外，有时摘录分开环绕在实际的文章中的重要的 markdown 语法。 因此这些摘录适用于一般性指导原则。 摘录仅使你能够知道您的兴趣是否值得花些时间后，单击，访问实际的文章。

有关这些和其他原因，不从这些摘录中，复制代码并不会为确切真实任何文本摘录。 相反，请访问实际的文章。



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-configure-sles-cluster-for-sql-server-availability-groupsql-server-linux-availability-group-cluster-slesmd"></a>1.&nbsp;[用于 SQL Server 可用性组配置 SLES 群集](sql-server-linux-availability-group-cluster-sles.md)

*Updated: 2017-06-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 189.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f8d28af253be1dc67615f1ea04135b2f6dff3b71 8be07deddcf0c348d75bf5b4f44615c2383e0722  (PR=2150  ,  Filename=sql-server-linux-availability-group-cluster-sles.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=6dccaff93a6c8b2374a1fad069b2f597898802fc) -->



**设置群集属性为 false 开始失败-是-严重**


`Start-failure-is-fatal`指示是否无法在节点上启动资源将阻止进一步开始尝试在该节点上。 当设置为`false`，群集将决定是否要尝试恢复使用基于资源的当前故障计数和迁移阈值的同一节点上启动。 因此，故障转移发生后，在 SQL 实例可用时，Pacemaker 将重新尝试在先前主节点上启动可用性组资源。 Pacemaker 负责将此副本降级为次要副本，并自动重新加入可用性组。 此外，如果`start-failure-is-fatal`设置为`false`，群集将回退到使用迁移阈值配置，因此你需要相应地更新迁移阈值，请确保默认的配置的 failcount 限制。

若要将属性值更新为 false，请运行：
```
sudo crm configure property start-failure-is-fatal=false
sudo crm configure rsc_defaults migration-threshold=5000
```
如果属性具有的默认值`true`，如果第一次尝试启动资源故障、 用户干预的清理资源失败计数自动故障转移后需要并且重置配置使用：`sudo crm resource cleanup <resourceName>`命令。

有关 Pacemaker 群集属性的详细信息，请参阅[配置群集资源](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html)。

**配置隔离 (STONITH)**

Pacemaker 群集供应商需要启用 STONITH，并对支持的群集安装程序配置隔离设备。 群集资源管理器无法确定节点或节点上资源的状态时，将使用隔离使群集再次处于已知状态。
资源级别隔离主要确保在因配置资源引起服务中断时，不会发生数据损坏。 例如，可将资源级别隔离用于 DRBD（分布式复制块设备），从而在通信链接出现故障时将节点上的磁盘标记为过时。




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>2.&nbsp;[有关在 Linux 上的 SQL Server 2017 发行说明](sql-server-linux-release-notes.md)

*Updated: 2017-06-20* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1))

<!-- Source markdown line 156.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 684da20f7834000886d7a93f83563c55dc3cf9a6 8597bcde7e5754bb7f38de1ec980027245dac6e5  (PR=2115  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=424a23fd98876db808b91f017e7acbcb5b4daa45) -->



**SQL Server Integration Services (SSIS)**

你可以在 Linux 上运行 SSIS 包。 有关详细信息，请参阅[博客文章宣布推出适用于 Linux 的 SSIS 支持](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。 请注意此版本中的以下已知的问题。

- **Mssql 服务器是**此时中，将包仅支持在 Ubuntu 上。

- 在 Linux 上运行 SSIS 包时，不支持以下功能：
  - SSIS 目录数据库
  - SQL 代理计划包执行
  - Windows 身份验证
  - 第三方组件
  - 第三方 ODBC 驱动程序
  - ODBC 连接管理器、 源和目标 （在 Linux CTP 2.1 刷新的 SSIS 支持）
  - 变更数据捕获 (CDC)
  - 扩展
  - Azure 功能包
  - Hadoop 和 HDFS 支持
  - Microsoft Connector for SAP BW

借助 Linux CTP 2.1 刷新的 SSIS，SSIS 包可以在 Linux 上使用 ODBC 连接。 有关详细信息，请参阅[博客文章在 Linux 上的宣布推出的 ODBC 支持](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。





<a name="similars2"/>

&nbsp;

## <a name="similar-articles"></a>类似的文章

本部分列出了一些相同的 GitHub.com 存储库中的其他使用者区域中的最近更新项目非常相似文章： [MicrosoftDocs /**sql 文档 pr**](https://github.com/microsoftdocs/sql-docs-pr/)。

<!--  20170717-1101  -->

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域它们具有新的或最近已更新的文章

- [新 + 更新 (4 + 4): **sql 高级分析**文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (2 + 0): **Analysis Services for SQL**文档](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (1 + 2):**连接到 SQL**文档](../connect/new-updated-connect.md)
- [新 + 更新 (6 + 0): **sql 数据库引擎**文档](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (13 + 2): **sql Linux**文档](../linux/new-updated-linux.md)
- [新 + 更新 (1 + 0): **sql 的 Master Data Services (MDS)**文档](../master-data-services/new-updated-master-data-services.md)
- [新 + 更新 (1 + 0): **sql 的 ODBC （开放式数据库连接）**文档](../odbc/new-updated-odbc.md)
- [新 + 更新 (8 + 4): **sql 的关系数据库**文档](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (2 + 2): **Microsoft SQL Server**文档](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (0 + 1): **SQL Server Management Studio (SSMS)**文档](../ssms/new-updated-ssms.md)
- [新 + 更新 (1 + 0): **TRANSACT-SQL**文档](../t-sql/new-updated-t-sql.md)
- [新 + 更新 (1 + 0): **SQL 的工具**文档](../tools/new-updated-tools.md)


#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>主题区域的任何新的或最近已更新的文章

- [新 + 更新 (0 + 0): **ActiveX 数据对象 (ADO) sql**文档](../ado/new-updated-ado.md)
- [新 + 更新 (0 + 0): **sql Data Quality Services**文档](../data-quality-services/new-updated-data-quality-services.md)
- [新 + 更新 (0 + 0):**数据挖掘扩展插件 (DMX) sql**文档](../dmx/new-updated-dmx.md)
- [新 + 更新 (0 + 0): **sql Integration Services**文档](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (0 + 0):**多维表达式 (MDX) sql**文档](../mdx/new-updated-mdx.md)
- [新 + 更新 (0 + 0):**适用于 SQL PowerShell**文档](../powershell/new-updated-powershell.md)
- [新 + 更新 (0 + 0): **sql Reporting Services**文档](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (0 + 0): **SQL 的示例**文档](../sample/new-updated-sample.md)
- [新 + 更新 (0 + 0): **SQL Server Data Tools (SSDT)**文档](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (0 + 0): **SQL Server 迁移助手 (SSMA)**文档](../ssma/new-updated-ssma.md)
- [新 + 更新 (0 + 0): **SQL 的 XQuery**文档](../xquery/new-updated-xquery.md)


&nbsp;


