---
title: "已更新-连接到 SQL Server 文档 |Microsoft 文档"
description: "显示有关最近更改中的文档，为连接到 Microsoft SQL Server 的更新内容的代码段。"
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: connect
ms.date: 02/03/2018
ms.openlocfilehash: cc4eb05dc4dcd74623c8ce7dfa7b7842449d79b6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-connect-to-sql-server"></a>新的和最近的更新： 连接到 SQL Server



几乎每日 Microsoft 及其现有的文章的一些上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文档网站。 这篇文章显示摘录最近已更新的文章。 可能还会列出链接到新的文章。

定期重新运行程序生成这篇文章。 有时摘录可使用不完善格式，或出现 markdown 源文章中的说明。 此处永远不会显示图像。

报告的以下日期范围和主题的新的更新：



- *日期范围的更新：* &nbsp; **自 2017 年 1-12-03** &nbsp;到&nbsp; **2018年-02-03**
- *主题区域：* &nbsp; **连接到 SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新项目

单击以下链接可跳转到最近添加的新文章。


暂时无新文章列出。



&nbsp;

## <a name="updated-articles-with-excerpts"></a>与摘录更新的文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘自其正确的语义上下文的来自分隔。 此外，有时摘录分开环绕在实际的文章中的重要的 markdown 语法。 因此这些摘录适用于一般性指导原则。 摘录仅使你能够知道您的兴趣是否值得花些时间后，单击，访问实际的文章。

有关这些和其他原因，不从这些摘录中，复制代码并不会为确切真实任何文本摘录。 相反，请访问实际的文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 的最近更新的文章的列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [使用始终加密的 ODBC 驱动程序适用于 SQL Server](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-using-always-encrypted-with-the-odbc-driver-for-sql-serverodbcusing-always-encrypted-with-the-odbc-drivermd"></a>1.&nbsp;[使用始终加密的 ODBC 驱动程序适用于 SQL Server](odbc/using-always-encrypted-with-the-odbc-driver.md)

*更新时间： 2018年-01-22* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 524.  ms.author= "v-chojas".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a52abae2a8f27c3b5bc411ef758610116a608f9f 352368eb269b98ab5ca3a9791fae2e70bf26277a  (PR=4686  ,  Filename=using-always-encrypted-with-the-odbc-driver.md  ,  Dirpath=docs\connect\odbc\  ,  MergeCommitSha40=82c9868b5bf95e5b0c68137ba434ddd37fc61072) -->



**检索使用 SQLGetData 部件中的数据**

对于 SQL Server，ODBC 驱动程序 17 加密之前字符和二进制列无法检索在使用 SQLGetData 部件中。 只有一个针对 SQLGetData 可以进行调用，使用具有足够的长度以包含整个列的数据缓冲区。

**在使用 SQLPutData 部件中发送数据**

插入或比较的数据不在使用 SQLPutData 部件中发送。 只有一个针对 SQLPutData 可以进行调用，使用包含整个数据的缓冲区。 用于插入到加密列的长整型数据，使用大容量复制 API，与输入的数据文件中下一节中所述。

**加密的 money 和 smallmoney**

加密**money**或**smallmoney**列不能将参数作为目标，因为不具体 ODBC 数据类型映射到这些类型，从而导致操作数类型冲突错误。

**大容量复制加密列**


利用[SQL 大容量复制函数](odbc/../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)和**bcp**实用程序的支持功能始终加密 ODBC 驱动程序 17 自 SQL Server。 纯文本 （加密上插入和解密上检索） 和密码文本 （按原义传输） 都可以插入并使用大容量复制中 （bcp_ *） Api 检索和**bcp**实用程序。

- 若要检索已加密文本 （例如，对于大容量加载到另一个数据库） 的 varbinary （max） 窗体中，连接而无需`ColumnEncryption`选项 (或将其设置为`Disabled`) 和执行 BCP OUT 操作。

- 插入和检索纯文本，并允许驱动程序以透明方式执行加密和解密作为必需的设置`ColumnEncryption`到`Enabled`就足够了。 否则保持不变的 BCP API 的功能。

- 将已加密文本插入 varbinary （max） 的形式 （例如检索到的上面） 中，设置`BCPMODIFYENCRYPTED`选项设为 TRUE，然后执行 BCP IN 操作。 为了使生成的数据要解密，请确保目标列的 CEK 是最初从中获取密码相同。







## <a name="similar-articles-about-new-or-updated-articles"></a>有关新的或更新的文章的类似文章

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>主题区域的*执行*新或最近已更新的文章


- [新 + 更新 (1 + 3):&nbsp; **sql 高级分析**文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (0 + 1):&nbsp; **SQL 的分析平台系统**文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新 + 更新 (0 + 1):&nbsp; **连接到 SQL**文档](../connect/new-updated-connect.md)
- [新 + 更新 (0 + 1):&nbsp; **sql 数据库引擎**文档](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (12 + 1): **sql Integration Services**文档](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (6 + 2):&nbsp; **sql Linux**文档](../linux/new-updated-linux.md)
- [新 + 更新 (15 + 0):**适用于 SQL PowerShell**文档](../powershell/new-updated-powershell.md)
- [新 + 更新 (2 + 9):&nbsp; **sql 的关系数据库**文档](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (1 + 0):&nbsp; **sql Reporting Services**文档](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (1 + 1):&nbsp; **SQL 操作 Studio**文档](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新 + 更新 (1 + 1):&nbsp; **Microsoft SQL Server**文档](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)**文档](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)**文档](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 2):&nbsp; **TRANSACT-SQL**文档](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>使用者执行的区域*不*有任何新最近更新或文章


- [新文章和更新的文章 (0+0)：SQL 数据迁移助手 (DMA) 文档](../dma/new-updated-dma.md)
- [新 + 更新 (0 + 0): **ActiveX 数据对象 (ADO) sql**文档](../ado/new-updated-ado.md)
- [新文章和更新的文章 (0+0)：SQL Analysis Services 文档](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (0 + 0): **sql Data Quality Services**文档](../data-quality-services/new-updated-data-quality-services.md)
- [新 + 更新 (0 + 0):**数据挖掘扩展插件 (DMX) sql**文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新 + 更新 (0 + 0):**多维表达式 (MDX) sql**文档](../mdx/new-updated-mdx.md)
- [新 + 更新 (0 + 0): **sql 的 ODBC （开放式数据库连接）**文档](../odbc/new-updated-odbc.md)
- [新 + 更新 (0 + 0): **SQL 的示例**文档](../sample/new-updated-sample.md)
- [新 + 更新 (0 + 0): **SQL Server 迁移助手 (SSMA)**文档](../ssma/new-updated-ssma.md)
- [新文章和更新的文章 (0+0)：SQL 工具文档](../tools/new-updated-tools.md)
- [新 + 更新 (0 + 0): **SQL 的 XQuery**文档](../xquery/new-updated-xquery.md)


