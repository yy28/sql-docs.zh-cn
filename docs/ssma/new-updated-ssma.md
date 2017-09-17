---
title: "更新的 SSMA for SQL Server 文档 |Microsoft 文档"
description: "显示有关最近更改中的文档，为 SQL Server 迁移助手 (SSMA) 的 Microsoft SQL Server 的更新内容的代码段。"
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
ms.workload: ssma-sql-server-migration-assistant
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 68df82bc7da6d7ef5aed3522c06704fb92bb0982
ms.contentlocale: zh-cn
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-migration-assistant-ssma"></a>新的和最近的更新： SQL Server Migration Assistant (SSMA)



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- *日期范围的更新：* &nbsp; **自 2017 年 1-07-18** &nbsp;到&nbsp;**自 2017 年 1-09-11**
- *主题区域：* &nbsp; **SQL Server Migration Assistant**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

以下链接跳转到最近已添加的新项目。


暂时无新文章列出。



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分显示的摘自从最近出现了大规模更新的文章中收集的更新。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此 compact 列表提供了有关摘录部分中列出的所有更新的文章的链接。

1. [什么 &#39; s SSMA for DB2 中的新增功能 (DB2ToSQL)](#TitleNum_1)
2. [SQL Server Migration Assistant](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-what39s-new-in-ssma-for-db2-db2tosqldb2what-s-new-in-ssma-for-db2-db2tosqlmd"></a>1.&nbsp;[什么 &#39; s SSMA for DB2 中的新增功能 (DB2ToSQL)](db2/what-s-new-in-ssma-for-db2-db2tosql.md)

*更新时间： 2017年-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 24.  ms.author= "Shamikg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c5dfb378ac578f54935a8a1fa7194398f3631017 f4427d1857894ad348cef5c92fbf6b51d00ee652  (PR=3070  ,  Filename=what-s-new-in-ssma-for-db2-db2tosql.md  ,  Dirpath=docs\ssma\db2\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



**SSMA v7.4**

SSMA for DB2 的 v7.4 版本包含以下更改：
- **查询超时值**选项现已可用在源和目标架构对象发现期间。
![query timeout 选项.../media/query-timeout_red.png)

- 通过目标修补程序，根据客户反馈，改进了的质量和转换的度量值。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA v7.4 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本是要停止使用。

**SSMA v7.3**

SSMA for DB2 的 v7.3 版本包含以下更改：
- 改进的质量和转换度量值根据客户反馈的目标修补程序。
- SSMA 扩展性框架公开通过以下各项：
  - 导出到 SQL Server Data Tools (SSDT) 项目的功能。
    -   你现在可以将架构脚本从 SSMA 导出到 SSDT 项目。 可以使用架构脚本进行其他架构更改和部署你的数据库。
![另存为 SSDT 项目命令.../media/export-schema-scripts_red.png)
  - 可用于执行自定义转换供 SSMA 的库。
    - 你现在可以构造自定义的语法转换和先前未由 SSMA 处理的转换可以处理的代码。
      - 在此博客文章中，提供了有关如何构造的自定义转换器说明[扩展 SQL Server Migration Assistant 的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      - 用于转换的示例项目可以下载这个[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。

**SSMA 7.2 版**

SSMA for DB2 的 7.2 版版本包含以下更改：
- 改进的质量和转换度量值根据客户反馈的目标修补程序。
- 遥测功能增强以提供更好的数据点，以解决客户问题和改进 SSMA 的转换率。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-migration-assistantsql-server-migration-assistantmd"></a>2.&nbsp;[SQL Server Migration Assistant](sql-server-migration-assistant.md)

*更新时间： 2017年-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_1))

<!-- Source markdown line 36.  ms.author= "Shamikg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 340d718e85fa73c6722862a0a7ba90239b247389 b29f4be2b6d208fd6038c2f9e1c7f0b7bd6b9ed7  (PR=3070  ,  Filename=sql-server-migration-assistant.md  ,  Dirpath=docs\ssma\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



**支持的源和目标版本**

有关支持的源，请查看 SSMA 下载下载中心上的信息。

SSMA 支持以下目标版本。

- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Azure SQL Database
- 在 Windows 和 Linux （预览版） 上的 SQL Server 自 2017 年 1
- * * Azure SQL 数据仓库

* * 仅适用于 Oracle 的 SSMA 支持此目标。









## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本部分列出了一些非常类似文章中我们公共 GitHub.com 存储库中的其他主题区域的最近更新项目： [MicrosoftDocs/sql 文档](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新 + 更新 (3 + 12): **sql 高级分析**文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (5 + 0):**连接到 SQL**文档](../connect/new-updated-connect.md)
- [新 + 更新 (5 + 1): **sql 数据库引擎**文档](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (19 + 82): **sql Integration Services**文档](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (1 + 8): **sql Linux**文档](../linux/new-updated-linux.md)
- [新 + 更新 (12 + 1): **sql 的关系数据库**文档](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (0 + 1): **sql Reporting Services**文档](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (7 + 1): **Microsoft SQL Server**文档](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (1 + 1): **SQL Server Data Tools (SSDT)**文档](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (0 + 2): **SQL Server 迁移助手 (SSMA)**文档](../ssma/new-updated-ssma.md)
- [新 + 更新 (1 + 4): **SQL Server Management Studio (SSMS)**文档](../ssms/new-updated-ssms.md)
- [新 + 更新 (4 + 1): **TRANSACT-SQL**文档](../t-sql/new-updated-t-sql.md)
- [新 + 更新 (0 + 1): **SQL 的工具**文档](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新 + 更新 (0 + 0): **Analysis Services for SQL**文档](../analysis-services/new-updated-analysis-services.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新 + 更新 (0 + 0): **sql 的 Master Data Services (MDS)**文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../sample/new-updated-sample.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)



