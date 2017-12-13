---
title: "已更新 - SQL Server SSDT 文档 | Microsoft Docs"
description: "显示 Microsoft SQL Server 的 SQL Server Data Tools (SSDT) 文档中最近更新内容的片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.component: ssdt
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.openlocfilehash: 07bfbac52cdd7d118ffd58842fe2085d52265e6f
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>新的和最近更新的文章：SQL Server Data Tools (SSDT)



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：从 2017-09-28 到 2017-12-02&nbsp;&nbsp;&nbsp;
- 主题区域：&nbsp;**SQL Server Data Tools (SSDT)**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


暂时无新文章列出。



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

更新日期：2017-11-20 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 28.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7700cae7cafe1dac95c240b014f14d9c83e32be4 6416949beaee91da2f77dfebb9eb5ed363db4cb7  (PR=4032  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=7f8aebc72e7d0c8cff3990865c9f1316996a67d5) -->




**SSDT for Visual Studio 2017（15.4.0 预览版）**

内部版本号：14.0.16134.0

**新增功能**


此版本为 Visual Studio 2017 15.4 或更高版本中的 SQL Server 数据库、Analysis Services、Reporting Services 和 Integration Services 项目提供了独立的 Web 安装程序。

**安装程序**


- 允许用户在安装新的 SSDT for VS 2017 实例时设置昵称。
- 在未选择任何 VS 实例的情况下会隐藏安装程序的功能选择复选框。
- 根据客户反馈优化了安装程序的某些消息。
- 修复了安装程序不支持升级的问题。


**SSIS**


- 修复了安装 Azure 功能包后导入/导出向导无法列出数据源的问题。
- 修复了切换连接时编辑 SSIS Analysis Services 进程任务会引发异常的问题。
- 修复了在应用添加 __$command_id 列的 SQL 修补程序后 CDC 组件会中断的问题。
- 修复了面向旧版 SQL Server 时无法编辑和执行第三方包的问题。
- 修复了双击 DTSWizard.exe 并选择“平面文件源”时“平面文件源”配置对话框无法正确显示的问题。
- 修复了面向 SQL Server 2017 时包含 Azure 功能包任务/组件的包无法执行的问题。


**已知问题**

- 安装程序尚未本地化。
- 当 ExecuteOutOfProcess 设置为“True”时，SSIS 执行包任务不支持调试。 此问题仅适用于调试。 通过 DTExec.exe 或 SSIS 目录进行保存、部署和执行将不受影响。


**SSDT 17.3 for Visual Studio 2015**

内部版本号：14.0.61709.290

**新增功能**


**Analysis Services (AS)**

- 在 1400 个模型中启用了 Cosmos DB 和 HDI Spark。
- 表格数据源属性。
- 现在支持“空白查询”选项，用于在查询编辑器中为 1400 兼容级别的模型创建新查询。
- 1400 模式模型的查询编辑器现在支持保存查询，而系统不会自动处理新的表格。







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


