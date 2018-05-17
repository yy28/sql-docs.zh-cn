---
title: 已更新 - SQL Server 文档 | Microsoft Docs
description: 显示 SQL Serverl 文档中最近更改的更新内容片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: sql-server
ms.date: 04/28/2018
ms.openlocfilehash: 9ccf32a232b501bb3184786af0c48dc7214b1936
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-server-docs"></a>新文章和最近更新的文章：SQL Server 文档



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：2018-02-03 到 2018-04-28&nbsp;&nbsp;&nbsp;
- 主题领域：&nbsp;**SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [如何参与编辑 SQL Server 文档](sql-server-docs-contribute.md)
2. [SQL Server 隐私补充](sql-server-privacy.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [SQL Server 2012 Service Pack 发行说明](#TitleNum_1)
2. [SQL Server 2016 发行说明](#TitleNum_2)
3. [SQL Server 文档](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2012-service-pack-release-notessql-server-2012-sp4-release-notesmd"></a>1.&nbsp; [SQL Server 2012 Service Pack 发行说明](sql-server-2012-sp4-release-notes.md)

更新日期：2018-04-25 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一篇](#TitleNum_2))

<!-- Source markdown line 57.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ce108992ea942b4a11f30d67a1a52d7f26868caa a6269ba2cb2d3b3b54aebf5087dc4d513e476a96  (PR=5676  ,  Filename=sql-server-2012-sp4-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- **自动 Soft-NUMA 分区** – 在服务级别启动了跟踪标志 8079 后，会借助 SQL 2014 SP2 引入自动 [Soft-NUMA](https://msdn.microsoft.com/library/ms345357(SQL.120).aspx) 技术。 如果在启动期间启用了跟踪标志 8079，SQL Server 2014 SP2 会询问硬件布局，并在报告每个 NUMA 节点 8 个或多个 CPU 的系统上自动配置 Soft NUMA。 自动 Soft NUMA 行为是超线程（HT/逻辑处理器）感知。 通过提高侦听器数、缩放和网络与加密功能，其他节点的分区和创建会缩放后台处理。 建议首先测试自动 Soft NUMA 的工作负荷性能，然后再在生产中启用该技术。

Service Pack 3 发行说明


下载页面

- [SQL Server 2012 SP3 功能包](http://go.microsoft.com/fwlink/?linkid=615935)
- [SQL Server 2012 SP3 Express](http://go.microsoft.com/fwlink/?linkid=692144)

若要详细了解如何基于当前安装版本确定要安装的文件的位置和名称，请参阅 [SQL Server 2012 Service Pack 3 版本信息](https://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information)中的“选择正确的文件进行下载”部分。

Service Pack 2 发行说明


下载页面

- [SQL Server 2012 SP2 功能包](http://go.microsoft.com/fwlink/?LinkID=401008)
- [SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)

使用下表，基于您当前安装的版本识别要下载的文件的位置和名称。 下载页包含系统要求和基本安装说明。

|如果当前安装的版本是...|并且希望...|下载并安装...|



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-2016-release-notessql-server-2016-release-notesmd"></a>2.&nbsp; [SQL Server 2016 发行说明](sql-server-2016-release-notes.md)

更新日期：2018-04-27 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_1) | [下一篇](#TitleNum_3))

<!-- Source markdown line 25.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a15210866acf524dae49f3a7fd7957c9ffa6a78a 7257cb2017779242cbb8fa2b562f4b102502e942  (PR=5695  ,  Filename=sql-server-2016-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=d1c114b98fea55d2d4829dffdb25daf1b3f73dc2) -->



  本主题介绍 SQL Server 2016 版本的限制和问题，包括服务包。 有关新增功能的信息，请参阅 [《What's New in SQL Server 2016》](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2016)（SQL Server 2016 的新增功能）。

- 从**[评估中心](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)** 下载 SQL Server 2016
- Azure 虚拟机小：是否拥有 Azure 帐户？  然后转到 **[此处](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)** ，启动装有 SQL Server 2016 SP1 的虚拟机。
- 下载 SSMS：若要获取最新版本的 SQL Server Management Studio，请参阅“[下载 SQL Server Management Studio (SSMS)]”。

**<a name="bkmk_2016sp2"></a>SQL Server 2016 Service Pack 2 (SP2)**


SQL Server 2016 SP2 包括 2016 SP1 之后、CU8 之前（含 CU8）发布的所有累积更新。

- [Microsoft Download SQL Server 2016 Service Pack 2 (SP2)](https://go.microsoft.com/fwlink/?linkid=869608)
- 有关更新的完整列表，请参阅 [SQL Server 2016 Service Pack 2 版本信息](https://support.microsoft.com/help/4052908/sql-server-2016-service-pack-2-release-information)



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sql-server-documentationsql-server-technical-documentationmd"></a>3.&nbsp; [SQL Server 文档](sql-server-technical-documentation.md)

更新日期：2018-04-27 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_2))

<!-- Source markdown line 77.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0262010ba39785a6d46b42f8469fb17701f13008 c69a83236391d039381a93c65ebbb2efa53e11b8  (PR=5695  ,  Filename=sql-server-technical-documentation.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=d1c114b98fea55d2d4829dffdb25daf1b3f73dc2) -->




<!-- : : : m-r -->
**试用 SQL Server！**
- 从评估中心下载：[下载 SQL Server for Windows](http://go.microsoft.com/fwlink/?LinkID=829477)
- 从评估中心下载：下载 SQL Server Management Studio (SSMS)
- 从评估中心下载：下载 SQL Server Data Tools (SSDT)
- 创建虚拟机：[获取具有 SQL Server 的虚拟机](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)





## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新的文章的类似文章

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新文章和更新的文章 (11+6)：SQL 高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)&nbsp; &nbsp;
- [新文章和更新的文章 (18+0)：Analysis Services for SQL 文档](../analysis-services/new-updated-analysis-services.md)&nbsp; &nbsp;
- [新文章和更新的文章 (218+14)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新文章和更新的文章 (14+0)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)&nbsp; &nbsp;
- [新文章和更新的文章 (3+2)： SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)&nbsp; &nbsp;
- [新文章和更新的文章 (3+3)： Linux for SQL 文档](../linux/new-updated-linux.md)&nbsp; &nbsp;
- [新文章和更新的文章 (7+10)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)&nbsp; &nbsp;
- [新文章和更新的文章 (0+2)：Reporting Services for SQL 文档](../reporting-services/new-updated-reporting-services.md)&nbsp; &nbsp;
- [新文章和更新的文章 (1+3)：SQL Operations Studio 文档](../sql-operations-studio/new-updated-sql-operations-studio.md)&nbsp; &nbsp;
- [新文章和更新的文章 (2+3)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)&nbsp; &nbsp;
- [新文章和更新的文章 (1+1)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)&nbsp; &nbsp;
- [新文章和更新的文章 (5+2)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)&nbsp; &nbsp;
- [新文章和更新的文章 (0+2)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)&nbsp; &nbsp;
- [新文章和更新的文章 (1+1)：SQL 工具文档](../tools/new-updated-tools.md)&nbsp; &nbsp;



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>主题区域没有新的或最近更新的文章

- [新文章和更新的文章 (0+0)：SQL 分析平台系统文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../samples/new-updated-samples.md)
- [新的和更新的文章 (0+0)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)

