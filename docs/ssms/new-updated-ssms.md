---
title: "已更新 - 适用于 SQL Server 的 SSMS 文档 | Microsoft Docs"
description: "显示 SQL Server 的 SQL Server Management Studio (SSMS) 文档中最近更改的更新内容片段。"
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
ms.workload: ssms-sql-server-management-studio
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 917198902baf85f2bae57c9ade9f8d3e29dea357
ms.contentlocale: zh-cn
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>新的和最近更新的文章：适用于 SQL Server 的 SQL Server Management Studio (SSMS)



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：从 2017 年 7 月 18 日到 2017 年 9 月 11 日
- 主题区域： &nbsp; **SQL Server Management Studio (SSMS)**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [SQL Server Management Studio 中的输出窗口](output-window.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [下载 SQL Server Management Studio (SSMS)](#TitleNum_1)
2. [连接到 SQL Server 或 Azure SQL 数据库](#TitleNum_2)
3. [SQL Server Management Studio (SSMS) - 更改日志](#TitleNum_3)
4. [创建和更新数据库表](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-management-studio-ssmsdownload-sql-server-management-studio-ssmsmd"></a>1.&nbsp;[下载 SQL Server Management Studio (SSMS)](download-sql-server-management-studio-ssms.md)

更新日期：2017-08-07 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[下一篇](#TitleNum_2)）

<!-- Source markdown line 63.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 23260f301f86651061b47065bee43d42c92a7be4 0c2178d96b621b96bfcd2fbb782f24792debb407  (PR=2775  ,  Filename=download-sql-server-management-studio-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=3f12671ace99d5fefc199c7b1c2db31e5b3cfade) -->



SSMS 17.2 是 SQL Server Management Studio 的最新版本。 SSMS 的 17.x 一代提供对 SQL Server 2008 到 SQL Server 2017 几乎所有功能领域的支持。 版本 17.x 也支持 SQL Analysis Service PaaS。

版本 17.2 包括：

- 多重身份验证 (MFA)
  - 用于含多重身份验证的通用身份验证的多用户 Azure AD 身份验证（具有 MFA 的 UA）
  - 为含 MFA 的通用身份验证添加了新的用户凭据输入字段，以支持多用户身份验证。
- 连接对话框现在支持以下 5 种身份验证方法：
  - Windows 身份验证
  - SQL Server 身份验证
  - Active Directory - 含 MFA 支持的通用身份验证
  - Active Directory - 密码
  - Active Directory - 集成

- DacFx 向导的数据库导入/导出现在可以使用含 MFA 的通用身份认证。
- 有关 API 支持，请参阅 [IUniversalAuthProvider 接口](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)。
- 具有 MFA 的 Azure AD 通用身份验证使用的 ADAL 托管库已升级到 3.13.9 版本。
- 新 CLI 界面，支持用于 SQL 数据库和 SQL 数据仓库的 Azure AD 管理设置。

 有关 Active Directory 身份验证方法的详细信息，请参阅[使用 SQL 数据库和 SQL 数据仓库进行通用身份验证（MFA 的 SSMS 支持）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)和[配置 SQL Server Management Studio 的 Azure SQL 数据库多重身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure)。

- 输出窗口具有在对象资源管理器节点扩展期间运行的查询条目
- 为 Azure SQL 数据库启用了查看设计器
- SSMS 中的对象资源管理器脚本对象的默认脚本选项已更改：



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-connect-to-a-sql-server-or-azure-sql-databaseobjectconnect-to-an-instance-from-object-explorermd"></a>2.&nbsp;[接到 SQL Server 或 Azure SQL 数据库](object/connect-to-an-instance-from-object-explorer.md)

更新日期：2017-08-25 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_1) | [下一篇](#TitleNum_3)）

<!-- Source markdown line 40.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cfd72893c35c87df96dc8605807e542be28936e2 840981d3a115a15774a8e47ee2f6a0e5c4177b01  (PR=2961  ,  Filename=connect-to-an-instance-from-object-explorer.md  ,  Dirpath=docs\ssms\object\  ,  MergeCommitSha40=21f0cfd102a6fcc44dfc9151750f1b3c936aa053) -->



   ![firewall--../media/connect-to-server/new-firewall-rule.png)

1. 要创建防火墙规则并连接到服务器，请单击“确定”。

1. 成功连接后，服务器将出现在“对象资源管理器”中：

   ![connected--../media/connect-to-server/connected.png)

**后续步骤**


[设计、创建和更新表--../visual-db-tools/design-tables-visual-database-tools.md)

**另请参阅**


[SQL Server Management Studio (SSMS)--../sql-server-management-studio-ssms.md) [下载 SQL Server Management Studio (SSMS)--../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>3.&nbsp; [SQL Server Management Studio - 更改日志 (SSMS)](sql-server-management-studio-changelog-ssms.md)

更新日期：2017-08-07 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_2) | [下一篇](#TitleNum_4)）

<!-- Source markdown line 20.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1733ce3c556db1e51cb27bf830429f2c42e8f97e 2abb24fd6547e438181039d095cbad027473a57e  (PR=2775  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=3f12671ace99d5fefc199c7b1c2db31e5b3cfade) -->



本文提供有关 SSMS 的当前和以前版本的更新、改进和 bug 修复的详细信息。 下载 [下面的 SSMS 早期版本--#previous-ssms-releases)。

**[SSMS 17.2--download-sql-server-management-studio-ssms.md)**


公开发布 | 版本号：14.0.17177.0

**增强功能**


- 多重身份验证 (MFA)
  - 用于含多重身份验证的通用身份验证的多用户 Azure AD 身份验证（具有 MFA 的 UA）
  - 为含 MFA 的通用身份验证添加了新的用户凭据输入字段，以支持多用户身份验证。
- 连接对话框现在支持以下 5 种身份验证方法：
  - Windows 身份验证
  - SQL Server 身份验证
  - Active Directory - 含 MFA 支持的通用身份验证
  - Active Directory - 密码
  - Active Directory - 集成

- DacFx 向导的数据库导出/导入使用含 MFA 的通用身份验证。
- 有关 API 支持，请参阅 [IUniversalAuthProvider 接口](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)。
- 具有 MFA 的 Azure AD 通用身份验证使用的 ADAL 托管库已升级到 3.13.9 版本。
- 此外，加入了新 CLI 接口，支持用于 SQL 数据库和 SQL 数据仓库的 Azure AD 管理设置。

 有关 Active Directory 身份验证方法的详细信息，请参阅[使用 SQL 数据库和 SQL 数据仓库进行通用身份验证（MFA 的 SSMS 支持）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)和[配置 SQL Server Management Studio 的 Azure SQL 数据库多重身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure)。

- 输出窗口具有在对象资源管理器节点扩展期间运行的查询条目



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-create-and-update-database-tablesvisual-db-toolsdesign-tables-visual-database-toolsmd"></a>4.&nbsp;[创建和更新数据库表](visual-db-tools/design-tables-visual-database-tools.md)

更新日期：2017-08-25 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;[上一篇](#TitleNum_3)）

<!-- Source markdown line 30.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f63884ac2d04889e70c505cb5262c8dd81d73ee7 4b4c7aa5e8a0548405f02d11a66b722219fa78f0  (PR=2961  ,  Filename=design-tables-visual-database-tools.md  ,  Dirpath=docs\ssms\visual-db-tools\  ,  MergeCommitSha40=21f0cfd102a6fcc44dfc9151750f1b3c936aa053) -->



**创建表**


1. 右键单击数据库中的“表”节点，然后选择“新建” > “表”：

    ![New table--../media/design-tables/new-table.png)

1. 将 [columns--column-properties-visual-database-tools.md) 添加到你的表：

    ![design table--../media/design-tables/new-table2.png)

1. 关闭设计器并保存更改。

**更新表**


1. 右键单击数据库的“表”节点下的表，并选择“设计”：

   ![Update table--../media/design-tables/update-table.png)

1. 更新所需的表设置：

   ![--../media/design-tables/update-table2.png)

1. 关闭设计器并保存更改。

**另请参阅**


[表](http://msdn.microsoft.com/82d7819c-b801-4309-a849-baa63083e83f) [Table Properties &#40;Visual Database Tools&#41;--../../ssms/visual-db-tools/table-properties-visual-database-tools.md) [Column Properties--column-properties-visual-database-tools.md) [Add Columns to a Table--../../relational-databases/tables/add-columns-to-a-table-database-engine.md) [Primary and Foreign Keys--../../relational-databases/tables/primary-and-foreign-key-constraints.md) [Indexes--../../relational-databases/indexes/indexes.md) [Data types (Transact-SQL)--../../t-sql/data-types/data-types-transact-sql.md) [Download SQL Server Management Studio (SSMS)--../download-sql-server-management-studio-ssms.md)







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



