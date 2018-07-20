---
title: 已更新-SQL Operations Studio 文件 |Microsoft 文件
description: 显示文档中最近更改，为 SQL Operations Studio 的更新内容片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: conceptual
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.date: 04/28/2018
ms.openlocfilehash: 84ee3d7d346c8cddbf5251e0d63bb2ae222defb3
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39083449"
---
# <a name="new-and-recently-updated-sql-operations-studio-docs"></a>新的和最近更新的文章： SQL Operations Studio 文档



几乎每日 Microsoft 及其现有的文章的一些上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文档网站。 这篇文章显示摘录最近已更新的文章。 可能还会列出链接到新的文章。

定期重新运行程序生成这篇文章。 有时摘录可使用不完善格式，或出现 markdown 源文章中的说明。 此处永远不会显示图像。

报告的以下日期范围和主题的新的更新：



- 更新日期范围：2018-02-03 到 2018-04-28&nbsp;&nbsp;&nbsp;
- *主题区域：* &nbsp; **SQL Operations Studio**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新项目

单击以下链接可跳转到最近添加的新文章。


- [扩展 SQL Operations Studio （预览版） 的功能](extensions.md)

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

1. [下载并安装 SQL Operations Studio （预览版）](#TitleNum_1)
2. [SQL Operations Studio （预览版） 发行说明](#TitleNum_2)
3. [教程： 添加*五个最慢的查询*示例小组件设为数据库仪表板](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-and-install-sql-operations-studio-previewdownloadmd"></a>1.&nbsp; [下载并安装 SQL Operations Studio （预览版）](download.md)

更新日期：2018-04-25 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一篇](#TitleNum_2))

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

### <a name="2-nbsp-sql-operations-studio-preview-release-notesrelease-notesmd"></a>2.&nbsp; [SQL Operations Studio （预览版） 发行说明](release-notes.md)

*更新日期： 2018年-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 20.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e2901d8a197f375f7d10ec93cbc9320362bf9278 0dde1aceceb339cb4cacd744e469f3d85d589668  (PR=5676  ,  Filename=release-notes.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**[下载年 4 月公共预览版]**


**2018 年 4 月 （年 4 月公共预览版）**


发布日期： 2018 年 4 月 25 日版本： 0.28.6

*年 4 月公共预览版*包含 bug 修复和改进。

- SQL 代理预览版扩展的改进。
- 改进了大型和受保护的文件是否支持保存受保护的管理员和 > 在 SQL Operations Studio 256 亿个文件。
- 集成的终端中拆分，以在一次处理多个打开终端。
- 减少的安装磁盘上的文件计数英尺打印速度更快的安装和启动时间。
- 继续修复 GitHub 问题：
   - 修复[发出 37](https://github.com/Microsoft/sqlopsstudio/issues/37)： 时，图表查看器引发错误，会发生意外的行为。
   - 修复[发出 462](https://github.com/Microsoft/sqlopsstudio/issues/462)： 功能请求： 默认情况下展开服务器组的选项。
   - 修复[发出 606](https://github.com/Microsoft/sqlopsstudio/issues/606): intellisense 的更新命令的糟糕的建议。
   - 修复[发出 967](https://github.com/Microsoft/sqlopsstudio/issues/967)： 预期的查询计划时在结果网格中选择 XML 显示计划。
   - 修复[发出 1023年](https://github.com/Microsoft/sqlopsstudio/issues/1023)： 从 flyfishingdba 添加 ms_foreachdb 调用的方括号。
   - 修复[发出 1048年](https://github.com/Microsoft/sqlopsstudio/issues/1048)： 预登录 SSL/TLS 握手错误。
   - 修复[发出 1050年](https://github.com/Microsoft/sqlopsstudio/issues/1050)： 清除 insights 查看之前显示错误。
   - 修复[发出 1057年](https://github.com/Microsoft/sqlopsstudio/issues/1057)： 还原和资源管理器小组件中的新查询操作被中断。



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboardtutorial-qds-sql-servermd"></a>3.&nbsp; [教程： 添加*五个最慢的查询*示例小组件设为数据库仪表板](tutorial-qds-sql-server.md)

更新日期：2018-04-25 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_2))

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
- [新 + 更新 (0 + 0): **sql Data Quality Services**文档](../data-quality-services/new-updated-data-quality-services.md)
- [新 + 更新 (0 + 0):**数据挖掘扩展插件 (DMX) sql**文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新 + 更新 (0 + 0):**多维表达式 (MDX) sql**文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新 + 更新 (0 + 0): **SQL 的示例**文档](../samples/new-updated-samples.md)
- [新 + 更新 (0 + 0): **SQL Server 迁移助手 (SSMA)** 文档](../ssma/new-updated-ssma.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)

