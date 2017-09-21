---
title: "已更新 - 关系数据库文档 | Microsoft Docs"
description: "显示关系数据库文档中最近更改的更新内容片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: ee7d66bcd8720234f4aec97d24ce16ed21888a3c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>新文章和最近更新的文章：关系数据库文档



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：从 2017-07-18 到 2017-09-11
- 主题领域：&nbsp; 关系数据库。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [将 Excel 数据导入 SQL Server 或 Azure SQL 数据库](import-export/import-data-from-excel-to-sql.md)
2. [PolyBase Kerberos 连接疑难解答](polybase/polybase-troubleshoot-connectivity.md)
3. [透明数据加密 (TDE)](security/encryption/transparent-data-encryption.md)
4. [用于 Azure SQL 数据库和数据仓库的透明数据加密](security/encryption/transparent-data-encryption-azure-sql.md)
5. [使用 Azure SQL 数据库和数据仓库的自带密钥支持进行透明数据加密](security/encryption/transparent-data-encryption-byok-azure-sql.md)
6. [PowerShell：使用 Azure Key Vault 中的自有密钥启用透明数据加密](security/encryption/transparent-data-encryption-byok-azure-sql-configure.md)
7. [使用 PowerShell 轮换透明数据加密 (TDE) 保护程序](security/encryption/transparent-data-encryption-byok-azure-sql-key-rotation.md)
8. [使用 PowerShell 删除透明数据加密 (TDE) 保护程序](security/encryption/transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)
9. [SQL Server 共享管理对象 (SMO) 许可条款](server-management-objects-smo/smo-license-terms.md)
10. [sys.external_libraries (Transact-SQL)](system-catalog-views/sys-external-libraries-transact-sql.md)
11. [sys.external_library_files (Transact-SQL)](system-catalog-views/sys-external-library-files-transact-sql.md)
12. [sp_rxPredict](system-stored-procedures/sp-rxpredict-transact-sql.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分显示从最近大幅更新的文章中收集到的更新的摘录内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表提供了在摘要部分列出的所有更新文章的链接。

1. [自动优化](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-automatic-tuningautomatic-tuningautomatic-tuningmd"></a>1.&nbsp;[自动优化](automatic-tuning/automatic-tuning.md)

更新日期：2017-08-16&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 

<!-- Source markdown line 64.  ms.author= "jovanpop".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 be765a1acf9bdfd5485520d16160677583e81f8e 135d926227094374e6ec5484e7babee625b44bb2  (PR=2860  ,  Filename=automatic-tuning.md  ,  Dirpath=docs\relational-databases\automatic-tuning\  ,  MergeCommitSha40=e4a6157cb56c6db911406585f841046a431eef99) -->



**自动计划选择更正**


每当检测到计划选择回归时，..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] 可自动切换到最近一个已知的良好计划。

![SQL plan choice correction--media/force-last-good-plan.png "SQL plan choice correction")

..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] 自动检测任何潜在的计划选择回归，包括应使用的计划（而不是错误计划）。
当 ..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] 应用最近一个已知的良好计划时，会自动监视强制计划的性能。 如果强制计划不比回归计划更好，则取消强制使用新计划，且 ..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] 会编译一个新计划。 如果 ..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] 证实强制计划优于回归计划，则会在重新编译（如下一次统计信息或架构更改时）之前保留此优于回归计划的强制计划。

**启用自动计划选择更正**


可以针对每个数据库启用自动优化，并指定在每次检测到某些计划更改回归时强制使用最近一个良好计划。 使用以下命令启用自动优化：

```
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON );
```
启用此选项后，..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] 自动强制使用具有以下特征的任何建议：估计的 CPU 性能提升超过 10 秒、或新计划中的错误数多于建议计划中的错误数，且经验证强制计划优于当前计划。

**替代项 - 手动计划选择更正**


若不使用自动优化，用户必须定期监视系统并查找回归的查询。 如果回归了任何计划，用户应找到某些计划







## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新文章和更新的文章 (3+12)：SQL 高级分析 文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章和更新的文章 (5+0)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新文章和更新的文章 (5+1)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新文章和更新的文章 (19+82)：SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)
- [新文章和更新的文章 (1+8)：Linux for SQL 文档](../linux/new-updated-linux.md)
- [新文章和更新的文章 (12+1)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新文章和更新的文章 (0+1)：SQL Reporting Services 文档](../reporting-services/new-updated-reporting-services.md)
- [新文章和更新的文章 (7+1)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新文章和更新的文章 (1+1)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新文章和更新的文章 (0+2)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新文章和更新的文章 (1+4)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新文章和更新的文章 (4+1)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)
- [新文章和更新的文章 (0+1)：Tools for SQL 文档](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新文章和更新的文章 (0+0)：SQL Analysis Services 文档](../analysis-services/new-updated-analysis-services.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../sample/new-updated-sample.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)



