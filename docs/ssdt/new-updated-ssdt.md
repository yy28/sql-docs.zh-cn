---
title: "已更新 - SQL Server SSDT 文档 | Microsoft Docs"
description: "显示 Microsoft SQL Server 的 SQL Server Data Tools (SSDT) 文档中最近更新内容的片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 8ae9a49443525524cf7f6ffceba4fb44984c7052
ms.contentlocale: zh-cn
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>新的和最近更新的文章：SQL Server Data Tools (SSDT)



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：从 2017 年 7 月 18 日到 2017 年 9 月 11 日
- 主题区域：&nbsp;**SQL Server Data Tools (SSDT)**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [SQL Server Data Tools - 许可条款](sql-server-data-tools-license-terms-vs2017.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [SQL Server Data Tools (SSDT) 的更改日志](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd"></a>1.&nbsp; [SQL Server Data Tools (SSDT) 的更改日志](changelog-for-sql-server-data-tools-ssdt.md)

更新日期：2017-08-23 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 23.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 536fe0fe41b023a4186f494a509fa14fcbafccf4 e5bc7b76c1755f5a1af77f6cd63d8e8691dafe7b  (PR=2927  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=71a2cbf181c94c4c1aff877614aadf890b2496e0) -->



**SSDT for Visual Studio 2017（15.3.0 预览版）**

内部版本号：14.0.16121.0

**新增功能**


此预览版是 SSDT for Visual Studio 2017 的第一个版本。 此版本为 Visual Studio 2017 15.3 及以上版本中的 SQL Server 数据库、Analysis Services、Reporting Services 和 Integration Services 项目引入了独立的 Web 安装体验。


**已知问题**

- 安装程序尚未本地化。
- SSIS 尚未本地化。
- 当 ExecuteOutofProcess 设置为 True 时，SSIS 执行包任务不支持调试。 此问题仅适用于调试。 通过 DTExec.exe 或 SSIS 目录进行保存、部署和执行将不受影响。
- 有关更改的完整列表，请参阅 [changelog--changelog-for-sql-server-data-tools-ssdt.md)。
- 若要报告问题，请访问 [SSDT Connect 反馈](https://connect.microsoft.com/SQLServer/Feedback)网站。
- 不可将包含第三方扩展的 SSIS 包切换为面向其他服务器版本。


**SSDT 17.2 for Visual Studio 2015**

内部版本号：14.0.61707.300

**新增功能**



**AS 项目：**
- 现在可以在“角色”对话框中配置“对象级安全性”，以便在 1400 个兼容级别表格模型中实现高级安全性。
- 用于在适用于 VS2017 的 SSDT AS 项目中的 AS Azure 模型中无电子邮件地址用户的新的 AAD 角色成员选择。
- SSDT AS 表格项目中新的 AS Azure“始终提示”项目属性，用于自定义 ADAL 凭据缓存的行为。


**Bug 修复**


**常规**
- 更新了适用于 SQL Server 2017 的品牌引用。

**AS 项目**
- 为增强提交 DAX 测量更改和其他模型编辑时的体验进行了显著的性能修复。
- 修复了使用 1400-兼容级别表格模型的 Analysis Services 项目中的 PowerQuery 集成的大量相关问题。
- 修复了在 VS2017 多维度项目中“设计聚合”设计器可能无法加载的问题。







## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本部分列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 中其他主题区域最近更新的非常相似文章。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新发布文章+最近更新的文章 (3+12)：SQL 高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新发布文章+最近更新的文章 (5+0)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新发布文章+最近更新的文章 (5+1)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新发布文章+最近更新的文章 (19+82)：SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)
- [新发布文章+最近更新的文章 (1+8)：Linux for SQL 文档](../linux/new-updated-linux.md)
- [新发布文章+最近更新的文章 (12+1)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新发布文章+最近更新的文章 (0+1)：SQL Reporting Services 文档](../reporting-services/new-updated-reporting-services.md)
- [新发布文章+最近更新的文章 (7+1)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新发布文章+最近更新的文章 (1+1)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新发布文章+最近更新的文章 (0+2)：SQL Server 迁移助手 (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新发布文章+最近更新的文章 (1+4)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新发布文章+最近更新的文章 (4+1)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)
- [新发布文章+最近更新的文章 (0+1)：Tools for SQL 文档](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新发布文章+最近更新的文章 (0+0)：SQL Analysis Services 文档](../analysis-services/new-updated-analysis-services.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新发布文章+最近更新的文章 (0+0)：SQL Master Data Services (MDS) 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../sample/new-updated-sample.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)



