---
title: 已更新-SQL Operations Studio 文件 |Microsoft 文件
description: 显示更新内容的 SQL 操作 Studio 中最近更改文档的代码的段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssops
ms.date: 04/28/2018
ms.openlocfilehash: 074ed6176480655d9d87a55eb87cbb76b3011b7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32686517"
---
# <a name="new-and-recently-updated-sql-operations-studio-docs"></a>新的和最近的更新： SQL 操作 Studio 文档



几乎每日 Microsoft 及其现有的文章的一些上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文档网站。 这篇文章显示摘录最近已更新的文章。 可能还会列出链接到新的文章。

定期重新运行程序生成这篇文章。 有时摘录可使用不完善格式，或出现 markdown 源文章中的说明。 此处永远不会显示图像。

报告的以下日期范围和主题的新的更新：



- *日期范围的更新：* &nbsp; **2018年-02-03** &nbsp;到&nbsp; **2018年-04-28**
- *主题区域：* &nbsp; **SQL 操作 Studio**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新项目

单击以下链接可跳转到最近添加的新文章。


- [扩展的功能的 SQL 操作 Studio （预览版）](extensions.md)

<!-- GeneMi:  I MANUALLY replace the ugly !INCLUDE with the name from inside the includes file. -->


&nbsp;

## <a name="updated-articles-with-excerpts"></a>与摘录更新的文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘自其正确的语义上下文的来自分隔。 此外，有时摘录分开环绕在实际的文章中的重要的 markdown 语法。 因此这些摘录适用于一般性指导原则。 摘录仅使你能够知道您的兴趣是否值得花些时间后，单击，访问实际的文章。

有关这些和其他原因，不从这些摘录中，复制代码并不会为确切真实任何文本摘录。 相反，请访问实际的文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 的最近更新的文章的列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [下载并安装 SQL 操作 Studio （预览版）](#TitleNum_1)
2. [SQL 操作 Studio （预览版） 发行说明](#TitleNum_2)
3. [教程： 添加*五个最慢的查询*示例小组件设为数据库仪表板](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-and-install-sql-operations-studio-previewdownloadmd"></a>1.&nbsp; [下载并安装 SQL 操作 Studio （预览版）](download.md)

*更新时间： 2018年-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 64.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6b4f80ad54c599e4354303a736f62e9715f99a32 18b22f464bbd8676348248ba5717b71acbab1c0d  (PR=5676  ,  Filename=download.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



   **Debian 安装：**
```
   cd ~
   sudo dpkg -i ./Downloads/sqlops-linux-<version string>.deb

   sqlops
```

   **rpm 安装：**
```
   cd ~
   yum install ./Downloads/sqlops-linux-<version string>.rpm

   sqlops
```

   **tar.gz 安装：**



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-operations-studio-preview-release-notesrelease-notesmd"></a>2.&nbsp; [SQL 操作 Studio （预览版） 发行说明](release-notes.md)

*更新时间： 2018年-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 20.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e2901d8a197f375f7d10ec93cbc9320362bf9278 0dde1aceceb339cb4cacd744e469f3d85d589668  (PR=5676  ,  Filename=release-notes.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**[下载年 4 月公共预览版]**


**年 4 月 2018 （年 4 月公共预览版）**


发布日期： 2018 年 4 月 25，版本： 0.28.6

*年 4 月公共预览版*包含 bug 修复和改进。

- 对 SQL 代理预览版扩展的改进。
- 改进了大型和受保护的文件是否支持保存受保护的管理员和 > 256 M SQL 操作 Studio 中的文件。
- 集成终端的拆分，若要同时使用多个打开终端。
- 减少的安装磁盘上的文件计数资源占用打印更快的安装和启动时间。
- 继续修复 GitHub 问题：
   - 修复[发出 37](https://github.com/Microsoft/sqlopsstudio/issues/37)： 当图表查看器引发错误时，会发生意外的行为。
   - 修复[发出 462](https://github.com/Microsoft/sqlopsstudio/issues/462)： 功能请求： 服务器组，默认情况下扩展的选项。
   - 修复[发出 606](https://github.com/Microsoft/sqlopsstudio/issues/606): intellisense 的更新命令的错误建议。
   - 修复[发出 967](https://github.com/Microsoft/sqlopsstudio/issues/967)： 预期查询计划时在结果网格中选择 XML 显示计划。
   - 修复[发出 1023年](https://github.com/Microsoft/sqlopsstudio/issues/1023)： 从 flyfishingdba 添加 ms_foreachdb 调用的方括号。
   - 修复[发出 1048年](https://github.com/Microsoft/sqlopsstudio/issues/1048)： 预登录 SSL/TLS 握手错误。
   - 修复[发出 1050年](https://github.com/Microsoft/sqlopsstudio/issues/1050)： 显示错误之前查看清除见解。
   - 修复[发出 1057年](https://github.com/Microsoft/sqlopsstudio/issues/1057)： 还原和新的查询操作，在资源管理器小组件已断开。



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboardtutorial-qds-sql-servermd"></a>3.&nbsp; [教程： 添加*五个最慢的查询*示例小组件设为数据库仪表板](tutorial-qds-sql-server.md)

*更新时间： 2018年-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_2))

<!-- Source markdown line 94.  ms.author= "erickang".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bc128acd966898cafc04381d7d83187d28466052 a47bf93ea4165618e0e514d7900ce1461f691aae  (PR=5676  ,  Filename=tutorial-qds-sql-server.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



       },
       {
           "name": "Tasks",
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 1
           },
           "widget": {
               "tasks-widget": {}
           }
       },
       {
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 2
           },
           "widget": {
               "explorer-widget": {}
           }







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新的文章的类似文章

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新 + 更新 (11 + 6): &nbsp; &nbsp; **sql 高级分析**文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (18 + 0): &nbsp; &nbsp; **Analysis Services for SQL**文档](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (218 + 14):**连接到 SQL**文档](../connect/new-updated-connect.md)
- [新 + 更新 (14 + 0): &nbsp; &nbsp; **sql 数据库引擎**文档](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (3 + 2): &nbsp; &nbsp; **sql Integration Services**文档](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (3 + 3): &nbsp; &nbsp; **sql Linux**文档](../linux/new-updated-linux.md)
- [新 + 更新 (7 + 10): &nbsp; &nbsp; **sql 的关系数据库**文档](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (0 + 2): &nbsp; &nbsp; **sql Reporting Services**文档](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (1 + 3): &nbsp; &nbsp; **SQL 操作 Studio**文档](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新 + 更新 (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server**文档](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** 文档](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** 文档](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 2): &nbsp; &nbsp; **TRANSACT-SQL**文档](../t-sql/new-updated-t-sql.md)
- [新 + 更新 (1 + 1): &nbsp; &nbsp; **SQL 的工具**文档](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>主题区域没有新的或最近更新的文章

- [新 + 更新 (0 + 0): **SQL 的分析平台系统**文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新 + 更新 (0 + 0): **sql Data Quality Services**文档](../data-quality-services/new-updated-data-quality-services.md)
- [新 + 更新 (0 + 0):**数据挖掘扩展插件 (DMX) sql**文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新 + 更新 (0 + 0):**多维表达式 (MDX) sql**文档](../mdx/new-updated-mdx.md)
- [新 + 更新 (0 + 0): **sql 的 ODBC （开放式数据库连接）** 文档](../odbc/new-updated-odbc.md)
- [新 + 更新 (0 + 0):**适用于 SQL PowerShell**文档](../powershell/new-updated-powershell.md)
- [新 + 更新 (0 + 0): **SQL 的示例**文档](../samples/new-updated-samples.md)
- [新 + 更新 (0 + 0): **SQL Server 迁移助手 (SSMA)** 文档](../ssma/new-updated-ssma.md)
- [新 + 更新 (0 + 0): **SQL 的 XQuery**文档](../xquery/new-updated-xquery.md)

