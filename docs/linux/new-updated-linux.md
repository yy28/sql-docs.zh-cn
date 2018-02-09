---
title: "已更新-Linux 文档上的 SQL Server |Microsoft 文档"
description: "显示有关最近更改中的文档，在 Linux 上的 Microsoft SQL server 的更新内容的代码段。"
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: linux
ms.date: 02/03/2018
ms.openlocfilehash: fc740b59397f0438a059b38df57ffc40999cc81e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>新的和最近的更新： Linux 文档上的 SQL Server



几乎每日 Microsoft 及其现有的文章的一些上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文档网站。 这篇文章显示摘录最近已更新的文章。 可能还会列出链接到新的文章。

定期重新运行程序生成这篇文章。 有时摘录可使用不完善格式，或出现 markdown 源文章中的说明。 此处永远不会显示图像。

报告的以下日期范围和主题的新的更新：



- *日期范围的更新：* &nbsp; **自 2017 年 1-12-03** &nbsp;到&nbsp; **2018年-02-03**
- *主题区域：* &nbsp; **在 Linux 上的 Microsoft SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新项目

单击以下链接可跳转到最近添加的新文章。


1. [配置多子网 Alwayson 可用性组和故障转移群集实例](sql-server-linux-configure-multiple-subnet.md)
2. [创建和配置 Linux 上的 SQL Server 的可用性组](sql-server-linux-create-availability-group.md)
3. [在 Linux 上的 SQL Server 的部署 Pacemaker 群集](sql-server-linux-deploy-pacemaker-cluster.md)
4. [在 Linux 上的 SQL Server 常见问题 (FAQ)](sql-server-linux-faq.md)
5. [SQL Server 可用性 Linux 部署的基础知识](sql-server-linux-ha-basics.md)
6. [在 Kubernetes 中配置 SQL Server 容器，以实现高可用性](tutorial-sql-server-containers-kubernetes.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>与摘录更新的文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘自其正确的语义上下文的来自分隔。 此外，有时摘录分开环绕在实际的文章中的重要的 markdown 语法。 因此这些摘录适用于一般性指导原则。 摘录仅使你能够知道您的兴趣是否值得花些时间后，单击，访问实际的文章。

有关这些和其他原因，不从这些摘录中，复制代码并不会为确切真实任何文本摘录。 相反，请访问实际的文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 的最近更新的文章的列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [Always On Linux 上的可用性组](#TitleNum_1)
2. [提取、 转换和加载使用 SSIS 的 Linux 上的数据](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-always-on-availability-groups-on-linuxsql-server-linux-availability-group-overviewmd"></a>1.&nbsp;[Always On Linux 上的可用性组](sql-server-linux-availability-group-overview.md)

*更新时间： 2018年-01-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 85.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 85685bc8ad3528aa26ca3f2bba7b0112808ad6f9 51aff6e55104c8f775d2b4f4461e44f689a9ee6b  (PR=4768  ,  Filename=sql-server-linux-availability-group-overview.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=d4d880dd9c247d1e7fb7a728d5231bc9ac61c989) -->



满足以下条件时，可能会自动故障转移的可用性组：

-   主和辅助副本设置为同步的数据移动。
-   辅助数据库已同步 （不同步），这意味着两个位于相同的数据点的状态。
-   群集类型设置为外部。 自动故障转移不能与群集类型为无。
-   `sequence_number`将成为辅助副本的主具有最高的序列号-换而言之，辅助副本的`sequence_number`匹配从原始主副本。

如果满足这些条件，承载主副本的服务器失败，则可用性组将将所有权更改为同步的副本。 同步副本的行为 (的其中可以有三个总： 一个主节点和两个辅助副本) 进一步可通过控制`required_synchronized_secondaries_to_commit`。 这在 Windows 和 Linux 上配合承载个可用性组，但配置完全不同。 在 Linux 上，通过该可用性组资源本身上的群集自动配置的值。

**仅配置副本和仲裁**


此外新在 SQL Server 自 2017 年截至 CU1 是仅配置副本。 因为 Pacemaker 不同于 WSFC，尤其是当涉及到仲裁和需要 STONITH，只需两个节点配置将无法工作时涉及到可用性组。 Fci，提供 Pacemaker 的仲裁机制可以是不错，因为所有 FCI 故障转移仲裁都发生在群集层。 对于可用性组，在 Linux 下的仲裁都会在 SQL Server 中，所有元数据的存储位置。 这是仅配置副本就会起作用。

如果没有任何其他内容，第三个节点和至少一个同步的副本将是所需。 这不适用于 SQL Server Standard，因为它可以仅有两个参与可用性组的副本。 仅配置副本存储在 master 数据库中，相同的可用性组配置中的其他副本 AG 配置。 仅配置副本没有参与可用性组的用户数据库。 从主来同步发送配置数据。 无论它们是自动还是手动的故障转移期间，然后使用此配置数据。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-extract-transform-and-load-data-on-linux-with-ssissql-server-linux-migrate-ssismd"></a>2.&nbsp;[提取、 转换和加载数据使用 SSIS 的 Linux 上](sql-server-linux-migrate-ssis.md)

*更新时间： 2018年-01-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_1))

<!-- Source markdown line 50.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9bba002ae3955ebb8376c7c85b7ec1ac8c706073 1533a8e0bfe553e5404de79129119b3f93185ee9  (PR=4768  ,  Filename=sql-server-linux-migrate-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=d4d880dd9c247d1e7fb7a728d5231bc9ac61c989) -->



    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  指定`/de[crypt]`选项输入密码以交互方式，如下面的示例中所示：

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de

    Enter decryption password:
    ```

3.  指定`/de`选项在命令行上提供的密码，如下面的示例中所示。 不推荐使用此方法，因为它将使用命令的解密密码存储中的命令历史记录。

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test

    Warning: Using /De[crypt] <password> may store decryption password in command history.

    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

**设计包**


**连接到 ODBC 数据源**。 借助上 Linux CTP 2.1 刷新及更高版本的 SSIS，SSIS 包可以在 Linux 上使用 ODBC 连接。 此功能已测试 SQL Server 和 MySQL ODBC 驱动程序，但还需要使用任何 Unicode ODBC 驱动程序观察到 ODBC 规范。 在设计时，你可以提供一个 DSN 或连接字符串以连接到 ODBC 数据中;你还可以使用 Windows 身份验证。 有关详细信息，请参阅[博客文章在 Linux 上的宣布推出的 ODBC 支持](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。







## <a name="similar-articles-about-new-or-updated-articles"></a>有关新的或更新的文章的类似文章

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>主题区域的*执行*新或最近已更新的文章


- [新 + 更新 (1 + 3):&nbsp; **sql 高级分析**文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (0 + 1):&nbsp; **SQL 的分析平台系统**文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新 + 更新 (0 + 1):&nbsp; **连接到 SQL**文档](../connect/new-updated-connect.md)
- [新 + 更新 (0 + 1):&nbsp; **sql 数据库引擎**文档](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (12 + 1): **sql Integration Services**文档](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (6 + 2):&nbsp; **sql Linux**文档](../linux/new-updated-linux.md)
- [新 + 更新 (15 + 0):**适用于 SQL PowerShell**文档](../powershell/new-updated-powershell.md)
- [新 + 更新 (2 + 9):&nbsp; **sql 的关系数据库**文档](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (1 + 0):&nbsp; **sql Reporting Services**文档](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (1 + 1):&nbsp; **SQL 操作 Studio**文档](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新 + 更新 (1 + 1):&nbsp; **Microsoft SQL Server**文档](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)**文档](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)**文档](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 2):&nbsp; **TRANSACT-SQL**文档](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>使用者执行的区域*不*有任何新最近更新或文章


- [新文章和更新的文章 (0+0)：SQL 数据迁移助手 (DMA) 文档](../dma/new-updated-dma.md)
- [新 + 更新 (0 + 0): **ActiveX 数据对象 (ADO) sql**文档](../ado/new-updated-ado.md)
- [新文章和更新的文章 (0+0)：SQL Analysis Services 文档](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (0 + 0): **sql Data Quality Services**文档](../data-quality-services/new-updated-data-quality-services.md)
- [新 + 更新 (0 + 0):**数据挖掘扩展插件 (DMX) sql**文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新 + 更新 (0 + 0):**多维表达式 (MDX) sql**文档](../mdx/new-updated-mdx.md)
- [新 + 更新 (0 + 0): **sql 的 ODBC （开放式数据库连接）**文档](../odbc/new-updated-odbc.md)
- [新 + 更新 (0 + 0): **SQL 的示例**文档](../sample/new-updated-sample.md)
- [新 + 更新 (0 + 0): **SQL Server 迁移助手 (SSMA)**文档](../ssma/new-updated-ssma.md)
- [新文章和更新的文章 (0+0)：SQL 工具文档](../tools/new-updated-tools.md)
- [新 + 更新 (0 + 0): **SQL 的 XQuery**文档](../xquery/new-updated-xquery.md)


