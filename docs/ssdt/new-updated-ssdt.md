---
title: 已更新 - SQL Server SSDT 文档 | Microsoft Docs
description: 显示 Microsoft SQL Server 的 SQL Server Data Tools (SSDT) 文档中最近更新内容的片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssdt
ms.date: 04/28/2018
ms.openlocfilehash: 99b0844803e1ce95bd6f73b0d45a2baf867428ba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>新的和最近更新的文章：SQL Server Data Tools (SSDT)



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：2018-02-03 到 2018-04-28&nbsp;&nbsp;&nbsp;
- 主题区域：&nbsp;**SQL Server Data Tools (SSDT)**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [SQL Server Data Tools (SSDT) 中的 Azure Active Directory 支持](azure-active-directory.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [SQL Server Data Tools (SSDT) 的更改日志](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd"></a>1.&nbsp; [SQL Server Data Tools (SSDT) 的更改日志](changelog-for-sql-server-data-tools-ssdt.md)

更新日期：2018-04-25 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 29.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 de18314845cffa197b3fd2ed868f2c330760bedb 5487de1ed57c16a6517a3a8849f412c208f1889f  (PR=5676  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->





**SSDT for Visual Studio 2017 (15.6.0)**

内部版本号：14.0.16162.0 发布日期：2018 年 4 月 10 日

**新增功能**


**SSIS：**

1.  修复问题：以 SQLServer2016 和 SQLServer2017 为目标时，AS 处理任务不记录任何处理步骤
2.  修复问题：在 SSDT 中打开具有很长非英文名称的 dtsx 时发生访问冲突
3.  修复问题：ScriptTask 变量列表有时会在任务 UI 中消失
4.  修复问题：当包位置为 SQL Server 时，添加现有包的副本失败
5.  修复问题：访问某个编辑器对话框中的组合框时，焦点会卡住。
6.  修复问题：切换 VS 主题时背景不更改。
7.  修复问题：注释和加载标签在深色主题中不可见。
8.  修复问题：SSIS 工具箱禁用项的状态属性定义不正确。
9.  修复问题：执行 WebServiceTask 始终失败。
10. 修复问题：如果连接字符串设置为某个变量，且其中包含依赖于项目参数的表达式，包部署会失败。

**安装程序：**

1.  在隐私免责声明中添加“SQL Server Data Tools 客户体验改善计划”链接。
2.  修复问题：当选择“安装新的 SQL Server Data Tools for Visual Studio 2017 实例”时会弹出 VS 安装程序窗口

已知问题：

1.  当 ExecuteOutOfProcess 设置为“True”时，SSIS 执行包任务不支持调试。 此问题仅适用于调试。 通过 DTExec.exe 或 SSIS 目录进行保存、部署和执行将不受影响。



SSDT for Visual Studio 2017 (15.5.2)

内部版本号：14.0.16156.0

**新增功能**


**SSIS**
1.  修复了 SSAS 和 SSIS 安装到同一 VS 2017 实例时，SSIS 2008 项目迁移会失败的问题。
2.  修复了 Rdlc 报表设计器和 SSIS 安装到同一 VS 2017 实例时，无法生成 Rdlc 项目的问题。







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

