---
title: "已更新 - SQL Server SSDT 文档 | Microsoft Docs"
description: "显示 Microsoft SQL Server 的 SQL Server Data Tools (SSDT) 文档中最近更新内容的片段。"
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: ssdt
ms.date: 02/03/2018
ms.openlocfilehash: c591ddddd60af31fe2d338fdee25ea2c17ab0ea5
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>新的和最近更新的文章：SQL Server Data Tools (SSDT)



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：2017-12-03 到 2018-02-03
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

更新日期：2018-01-18 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 28.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6416949beaee91da2f77dfebb9eb5ed363db4cb7 de18314845cffa197b3fd2ed868f2c330760bedb  (PR=4652  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



**SSDT for Visual Studio 2017 (15.5.1)**

内部版本号：14.0.16148.0

**新增功能**


除了安装程序的以下 bug 修复以外，Visual Studio 2017 (15.5.1) 与版本 15.5.0 相同：

1.  修复安装程序在 SQL Server Integration Services 安装后挂起的问题。
2.  修复安装失败并出现错误消息：“不支持请求的元文件操作(0x800707D3)”的问题。

除了这两个 bug 修复之外，以下有关 15.5.0 的详细信息也仍适用于 15.5.1

**SSDT for Visual Studio 2017 (15.5.0)**

内部版本号：14.0.16146.0

**新增功能**


SSDT for Visual Studio 2017 (15.5.0) 不再提供预览版，改为提供正式版 (GA)。

**安装程序**
1. 安装程序 UI 已本地化。
1. 将图标替换为更高质量的版本。

**Integration Services (IS)**
1. 在 ADF 中将包部署到 Azure SSIS IR 时，部署向导中添加了包验证步骤，可发现要在 Azure SSIS IR 中执行的 SSIS 包的潜在兼容性问题。 有关详细信息，请参阅[验证部署到 Azure 的 SSIS 包](..\integration-services\lift-shift\ssis-azure-validate-packages.md)。
1. SSIS 扩展已本地化。

**Bug 修复**


**Integration Services (IS)**
1. 修复了 OLEDB 和 ADO.NET 连接管理器的布局损坏的问题。
2. 修复了尝试编辑维度处理任务时出现程序集未发现已出现错误的问题。

**已知问题**


**Integration Services (IS)** 当 ExecuteOutOfProcess 设置为 True 时，SSIS 执行包任务不支持调试。 此问题仅适用于调试。 通过 DTExec.exe 或 SSIS 目录进行保存、部署和执行将不受影响。



**SSDT 17.4 for Visual Studio 2015**

内部版本号：14.0.61712.050

**新增功能**


**Analysis Services (AS) 项目**
- 向表格项目添加了三个新选项（在“选项”>“Analysis Services 表格”>“数据导入”下）：







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新的文章的类似文章

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章


- [新文章和更新的文章 (1+3)：SQL&nbsp;高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章和更新的文章 (0+1)：SQL&nbsp;分析平台系统文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章和更新的文章 (0+1)：连接到&nbsp;SQL 文档](../connect/new-updated-connect.md)
- [新文章和更新的文章 (0+1)：SQL&nbsp;数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新文章和更新的文章 (12+1)：SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)
- [新文章和更新的文章&nbsp;(6+2)：Linux for SQL 文档](../linux/new-updated-linux.md)
- [新文章和更新的文章 (15+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新文章和更新的文章&nbsp;(2+9)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新文章和更新的文章&nbsp;(1+0)：SQL Reporting Services 文档](../reporting-services/new-updated-reporting-services.md)
- [新文章和更新的文章&nbsp;(1+1)：SQL Operations Studio 文档](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章和更新的文章&nbsp;(1+1)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新文章和更新的文章&nbsp;(0+1)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新文章和更新的文章&nbsp;(1+2)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新文章和更新的文章&nbsp;(0+2)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>主题区域没有新的或最近更新的文章


- [新文章和更新的文章 (0+0)：SQL 数据迁移助手 (DMA) 文档](../dma/new-updated-dma.md)
- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新文章和更新的文章 (0+0)：SQL Analysis Services 文档](../analysis-services/new-updated-analysis-services.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../sample/new-updated-sample.md)
- [新的和更新的文章 (0+0)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新文章和更新的文章 (0+0)：SQL 工具文档](../tools/new-updated-tools.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)


