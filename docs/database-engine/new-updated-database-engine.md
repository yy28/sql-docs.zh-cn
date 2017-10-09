---
title: "更新内容 - 数据库引擎文档| Microsoft Docs"
description: "显示数据库引擎的文档中最近更改的更新内容片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: barbkess
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: database-engine
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: dc4a5516662b200b4224facbb4c9cf4588c1b42e
ms.contentlocale: zh-cn
ms.lasthandoff: 10/02/2017

---
# <a name="new-and-recently-updated-database-engine-docs"></a>新增内容和最近更新内容：数据库引擎文档



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：从 2017-09-11 到 2017-09-27&nbsp;&nbsp;&nbsp;
- 主题区域：&nbsp;数据库引擎。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [向 SQL Server 的实例添加功能（安装程序）](install-windows/add-features-to-an-instance-of-sql-server-setup.md)
2. [从命令提示符安装 SQL Server](install-windows/install-sql-server-from-the-command-prompt.md)
3. [使用配置文件安装 SQL Server](install-windows/install-sql-server-using-a-configuration-file.md)
4. [业务连续性和数据库恢复 - SQL Server](sql-server-business-continuity-dr.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [从命令提示符安装更新](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-installing-updates-from-the-command-promptinstall-windowsinstalling-updates-from-the-command-promptmd"></a>1.&nbsp; [从命令提示符安装更新](install-windows/installing-updates-from-the-command-prompt.md)

更新日期：2017-09-12&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 

<!-- Source markdown line 48.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 04abb23d0682c23654a55e7926d2140f0b6ae408 a4bb1e27ae99460a66da72848ace1417b148f85c  (PR=3122  ,  Filename=installing-updates-from-the-command-prompt.md  ,  Dirpath=docs\database-engine\install-windows\  ,  MergeCommitSha40=1df54edd5857ac2816fa4b164d268835d9713638) -->



- 在计算机和所有共享组件上安装 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 的所有实例，如 ..!NCLUDE-NotShown--ssISnoversion--../../includes/ssisnoversion-md.md)] 和管理工具：

```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances.
```

- 从 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 的单个实例和所有共享组件中删除更新，如 ..!NCLUDE-NotShown--ssISnoversion--../../includes/ssisnoversion-md.md)] 和管理工具：

```
    <package_name>.exe /qs /Action=RemovePatch /InstanceName=MyInstance.
```

- 仅从 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 共享组件中删除更新，如 ..!NCLUDE-NotShown--ssISnoversion--../../includes/ssisnoversion-md.md)] 和管理工具：

```
    <package_name>.exe /qs /Action=RemovePatch
```







## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新文章和更新的文章 (0+1)：SQL 高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章和更新的文章 (0+1)：SQL Analysis Services 文档](../analysis-services/new-updated-analysis-services.md)
- [新文章和更新的文章 (4+1)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新文章和更新的文章 (17+0)：SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)
- [新文章和更新的文章 (3+0)：Linux for SQL 文档](../linux/new-updated-linux.md)
- [新文章和更新的文章 (1+1)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新文章和更新的文章 (2+0)：SQL Reporting Services 文档](../reporting-services/new-updated-reporting-services.md)
- [新文章和更新的文章 (0+1)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新文章和更新的文章 (0+1)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新文章和更新的文章 (0+0)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../sample/new-updated-sample.md)
- [新文章和更新的文章 (0+0)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新的和更新的文章 (0+0)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新的和更新的文章 (0+0)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新文章和更新的文章 (0+0)：SQL 工具文档](../tools/new-updated-tools.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)



