---
title: "已更新 - 关系数据库文档 | Microsoft Docs"
description: "显示关系数据库文档中最近更改的更新内容片段。"
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: relational-databases
ms.date: 02/03/2018
ms.openlocfilehash: 38f9ee55137c54adddb07fbe9f3b74dd43d51a3a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>新文章和最近更新的文章：关系数据库文档



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：2017-12-03 到 2018-02-03
- 主题领域：&nbsp; 关系数据库。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [在 SQL Server 或 SQL 数据库中存储 JSON 文档](json/store-json-documents-in-sql-tables.md)
2. [SQL 漏洞评估](security/sql-vulnerability-assessment.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [数据库文件初始化](#TitleNum_1)
2. [tempdb 数据库](#TitleNum_2)
3. [SQL Server 中的 JSON 数据](#TitleNum_3)
4. [第 1 课：连接到数据库引擎](#TitleNum_4)
5. [管理事务日志文件的大小](#TitleNum_5)
6. [bcp_bind](#TitleNum_6)
7. [SQL Server 索引设计指南](#TitleNum_7)
8. [sp_execute_external_script (Transact-SQL)](#TitleNum_8)
9. [创建主键](#TitleNum_9)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-database-file-initializationdatabasesdatabase-instant-file-initializationmd"></a>1.&nbsp; [数据库文件初始化](databases/database-instant-file-initialization.md)

更新日期：2018-01-23 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  （[下一篇](#TitleNum_2)）

<!-- Source markdown line 81.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c5f2aa53a8b43d4c43e0602cf945cb7c7028a27d 04c261c6588af1f53cda2fce3e9a86167c50b686  (PR=4702  ,  Filename=database-instant-file-initialization.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=3206a31870f8febab7d1718fa59fe0590d4d45db) -->



```
Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

适用对象：SQL Server（从 SQL Server 2012 SP4、SQL Server 2014 SP2 和 SQL Server 2016 起，直到 SQL Server 2017）

**安全注意事项**

使用即时文件初始化 (IFI) 时，由于只有在新数据写入文件中时才覆盖删除的磁盘内容，因此，在数据文件的该特定区域中发生某些其他的数据写入前，未授权的主体可能会访问删除的内容。 当数据库文件连接到 SQL Server 实例之后，可以通过文件中的随机访问控制列表 (DACL) 来降低此信息泄露的风险。 此 DACL 仅允许 SQL Server 服务帐户和本地管理员访问文件。 但是，当文件分离以后，可以由不具有 SE\_MANAGE\_VOLUME_NAME 的用户或服务访问。 备份数据库时，将需要以下类似考虑：如果未使用适当的 DACL 对备份文件进行保护，则未授权的用户或服务将可以使用删除的内容。

另一个注意事项是，如果使用 IFI 增加文件大小，SQL Server 管理员可能会访问原始页面内容并查看以前删除的内容。

如果数据库文件托管在存储区域网络上，则存储区域网络也可能始终以预初始化方式呈现新页面，并且操作系统重新初始化页面可能导致不必要的开销。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-tempdb-databasedatabasestempdb-databasemd"></a>2. &nbsp; [tempdb 数据库](databases/tempdb-database.md)

更新日期：2018-01-17 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_1) | [下一篇](#TitleNum_3)）

<!-- Source markdown line 100.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 337555ea28f4c3fdd6b78f1bfb4d62607a6bf92d 3257c92d6e2a88968fc44e5f6262c02cd0624635  (PR=0  ,  Filename=tempdb-database.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=45e6082acc29ba306525e7c08d2c22cc2b86eec3) -->



 有关这些数据库选项的说明，请参阅 [ALTER DATABASE SET 选项 (Transact-SQL)](databases/../../t-sql/statements/alter-database-transact-sql-set-options.md)。

**SQL 数据库中的 Tempdb 数据库**


|SLO|最大 tempdb 数据文件大小 (MB)|tempdb 数据文件数|最大 tempdb 数据大小 (MB)|
|---|---:|---:|---:|
|“基本”|14,225|@shouldalert|14,225|
|S0|14,225|@shouldalert|14,225|
|S1|14,225|@shouldalert|14,225|
|S2|14,225| @shouldalert|14,225|
|S3|32,768|@shouldalert|32,768|
|S4|32,768|2|65,536|
|S6|32,768|3|98,304|
|S7|32,768|6|196,608|
|S9|32,768|12|393,216|
|S12|32,768|12|393,216|
|P1|32,768|12|393,216|
|P2|32,768|12|393,216|
|P4|32,768|12|393,216|
|P6|32,768|12|393,216|
|P11|32,768|12|393,216|
|P15|32,768|12|393,216|
|高级弹性池（所有 DTU 配置）|14,225|12|170,700|
|标准弹性池（所有 DTU 配置）|14,225|12|170,700|
|基本弹性池（所有 DTU 配置）|14,225|12|170,700|
||||




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-json-data-in-sql-serverjsonjson-data-sql-servermd"></a>3.&nbsp; [SQL Server 中的 JSON 数据](json/json-data-sql-server.md)

更新日期：2018-02-01 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_2) | [下一篇](#TitleNum_4)）

<!-- Source markdown line 233.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 62dd9c68d8cb72d6bf51b941a0731224514f0a7f 19e276637a463b412f2c29a84f9fb7d0b0f5fcc5  (PR=4783  ,  Filename=json-data-sql-server.md  ,  Dirpath=docs\relational-databases\json\  ,  MergeCommitSha40=73f18ae24a9a48234bf997ee9a2ef441bc4918b9) -->



-   [Loading GeoJSON data into SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/)（将 GeoJSON 数据加载到 SQL Server 2016）

**使用 SQL 查询分析 JSON 数据**

如果必须筛选或聚合 JSON 数据用于报表，可以使用 OPENJSON 将 JSON 转换为关系格式。 然后，可使用标准 Transact-SQL 和内置函数来准备报表。

```
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date
FROM   SalesOrderRecord AS Tab
          CROSS APPLY
     OPENJSON (Tab.json, N'$.Orders.OrdersArray')
           WITH (
              Number   varchar(200) N'$.Order.Number',
              Date     datetime     N'$.Order.Date',
              Customer varchar(200) N'$.AccountNumber',
              Quantity int          N'$.Item.Quantity'
           )
  AS SalesOrderJsonData
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified
```



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-lesson-1-connecting-to-the-database-enginelesson-1-connecting-to-the-database-enginemd"></a>4.&nbsp; [第 1 课：连接到数据库引擎](lesson-1-connecting-to-the-database-engine.md)

更新日期：2017-12-13 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_3) | [下一篇](#TitleNum_5)）

<!-- Source markdown line 79.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3c070935895450fd2ea054e2be9e1c48f7dc2b6c 0c386e3d47fb7f8f1e63b9301f0cafec2bc88ab0  (PR=4282  ,  Filename=lesson-1-connecting-to-the-database-engine.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=6e016a4ffd28b09456008f40ff88aef3d911c7ba) -->



2.  选择“数据库引擎”。

    ![object-explorer](../relational-databases/media/object-explorer.png)

3.  在“服务器名称”框中，键入数据库引擎实例的名称。 对于默认的 SQL Server 实例，服务器名称即计算机名称。 对于 SQL Server 的命名实例，服务器名称为 <computer_name>\\<instance_name>，如 ACCTG_SRVR\SQLEXPRESS。 以下屏幕截图显示如何连接到名为“PracticeComputer”的计算机上 SQL Server 的默认（未命名）实例。 已登录到 Windows 的用户是 Contoso 域中的 Mary。 使用 Windows 身份验证时，无法更改用户名称。

    ![connect-to-server](../relational-databases/media/connect-to-server.png)

4.  单击 **“连接”**。

> [!NOTE]
> 本教程假定用户刚接触 SQL Server，并且连接时没有出现特殊问题。 这应足以满足大多数人的需求，并使本教程保持简单。 有关疑难解答步骤的详细信息，请参阅 [对连接到 SQL Server 数据库引擎的疑难解答](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)。

**<a name="additional"></a>授权其他连接**

现在，已经以管理员身份连接到了 SQL Server，首要任务之一是授权其他用户进行连接。 实现此任务的步骤是创建一个登录名，然后授权此登录名以用户身份访问数据库。 登录名可以是使用 Windows 凭据的 Windows 身份验证登录名；也可以是 SQL Server 身份验证登录名（这些登录名在 SQL Server 中存储身份验证信息并独立于 Windows 凭据）。 尽可能使用 Windows 身份验证。



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-manage-the-size-of-the-transaction-log-filelogsmanage-the-size-of-the-transaction-log-filemd"></a>5.&nbsp; [管理事务日志文件的大小](logs/manage-the-size-of-the-transaction-log-file.md)

更新日期：2018-01-17 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_4) | [下一篇](#TitleNum_6)）

<!-- Source markdown line 105.  ms.author= "jhubbard".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5847b31cf8f6003a380f0c8aaa289efdc55be678 84e45320d81db218cde17fbf8b9668a9ac3805a7  (PR=0  ,  Filename=manage-the-size-of-the-transaction-log-file.md  ,  Dirpath=docs\relational-databases\logs\  ,  MergeCommitSha40=45e6082acc29ba306525e7c08d2c22cc2b86eec3) -->



-   小型的增长增量可能生成过多的 [VLF](logs/../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 并且可能降低性能。 若要确定给定实例中所有数据库的当前事务日志大小的最佳 VLF 分发，以及实现所需大小需要的增长量，请参阅此[脚本](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs)。

-   大型的增长增量可能生成过少的大型 [VLF](logs/../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 并且也可能影响性能。 若要确定给定实例中所有数据库的当前事务日志大小的最佳 VLF 分发，以及实现所需大小需要的增长量，请参阅此[脚本](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs)。

-   即使启用自动增长，如果增长速度不能满足查询需求，也可能收到提示事务日志已满的消息。 有关更改增长增量的详细信息，请参阅 [ALTER DATABASE (Transact-SQL) 文件和文件组选项](logs/../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)

-   在数据库中有多个日志文件不会以任何方式提升性能，因为事务日志文件不会像同一文件组中的数据文件一样使用[比例填充](logs/../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill)。

-   日志文件可以设为自动收缩。 但是，不建议这样做，auto_shrink 数据库属性默认设为 FALSE。 如果 auto_shrink 设置为 TRUE，则仅当其空间的 25% 以上未使用时，自动收缩才会减少文件的大小。



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-bcpbindnative-client-odbc-extensions-bulk-copy-functionsbcp-bindmd"></a>6. &nbsp; [bcp_bind](native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)

更新日期：2018-01-30 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_5) | [下一篇](#TitleNum_7)）

<!-- Source markdown line 127.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d50791cef948ce8b3066438e317ab4d34d535258 e6f70559e7237cfc86dfc5746d218c08bec52af6  (PR=4762  ,  Filename=bcp-bind.md  ,  Dirpath=docs\relational-databases\native-client-odbc-extensions-bulk-copy-functions\  ,  MergeCommitSha40=60006e90d03fdb75b282bbc0dad3d40571bacacc) -->



 下表列出了有效的枚举数据类型以及相应的 ODBC C 数据类型。

|eDataType|C 类型|
|-----------------------|------------|
|SQLTEXT|char *|
|SQLNTEXT|wchar_t *|
|SQLCHARACTER|char *|
|SQLBIGCHAR|char *|
|SQLVARCHAR|char *|
|SQLBIGVARCHAR|char *|
|SQLNCHAR|wchar_t *|
|SQLNVARCHAR|wchar_t *|
|SQLBINARY|unsigned char *|
|SQLBIGBINARY|unsigned char *|
|SQLVARBINARY|unsigned char *|
|SQLBIGVARBINARY|unsigned char *|
|SQLBIT|char|
|SQLBITN|char|
|SQLINT1|char|
|SQLINT2|short int|
|SQLINT4|ssNoversion|
|SQLINT8|_int64|
|SQLINTN|cbIndicator<br /> 1: SQLINT1<br /> 2: SQLINT2<br /> 4: SQLINT4<br /> 8: SQLINT8|
|SQLFLT4|FLOAT|
|SQLFLT8|FLOAT|
|SQLFLTN|cbIndicator<br /> 4: SQLFLT4<br /> 8: SQLFLT8|
|SQLDECIMALN|SQL_NUMERIC_STRUCT|
|SQLNUMERICN|SQL_NUMERIC_STRUCT|
|SQLMONEY|DBMONEY|
|SQLMONEY4|DBMONEY4|
|SQLMONEYN|cbIndicator<br /> 4: SQLMONEY4<br /> 8: SQLMONEY|
|SQLTIMEN|SQL_SS_TIME2_STRUCT|
|SQLDATEN|SQL_DATE_STRUCT|
|SQLDATETIM4|DBDATETIM4|
|SQLDATETIME|DBDATETIME|
|SQLDATETIMN|cbIndicator<br /> 4: SQLDATETIM4<br /> 8: SQLDATETIME|
|SQLDATETIME2N|SQL_TIMESTAMP_STRUCT|
|SQLDATETIMEOFFSETN|SQL_SS_TIMESTAMPOFFSET_STRUCT|
|SQLIMAGE|unsigned char *|
|SQLUDT|unsigned char *|
|SQLUNIQUEID|SQLGUID|
|SQLVARIANT|除以下数据类型之外的任意数据类型：<br />-   text<br />-   ntext<br />-   image<br />-   varchar(max)<br />-   varbinary(max)<br />-   nvarchar(max)<br />-   xml<br />-   timestamp|
|SQLXML|支持的 C 数据类型：<br />-   char*<br />-   wchar_t *<br />-   unsigned char *|



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-sql-server-index-design-guidesql-server-index-design-guidemd"></a>7.&nbsp; [SQL Server 索引设计指南](sql-server-index-design-guide.md)

更新日期：2018-01-02 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_6) | [下一篇](#TitleNum_8)）

<!-- Source markdown line 700.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bd09c9e66cd3cf5f3ebebe7ffa6e937978353169 8e5cbbf0063971676a8bafefba75aa5c7c28be61  (PR=0  ,  Filename=sql-server-index-design-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=74daee358fef75a25d75c69d971d08536c5bd2be) -->



从 SQL Server 2016 开始，可以对行存储表创建可更新的非聚集列存储索引。 列存储索引将存储数据的副本，因此你需要提供额外的存储。 但是，列存储索引中的数据压缩成的大小比行存储表所需的大小更小。  如果采取这种做法，你可以同时对列存储索引以及行存储索引上的事务运行分析。 当行存储表中的数据更改时，列存储将会更新，因此这两个索引适用于相同的数据。

从 SQL Server 2016 开始，可以对一个列存储索引使用一个或多个非聚集行存储索引。 这样，便可以针对基础列存储上执行有效的表查找。 其他选项也可供使用。 例如，可以通过在行存储表中使用 UNIQUE 约束来强制主键约束。 由于不唯一的值无法插入行存储表，SQL Server 无法将值插入列存储。

**性能注意事项**


-   非聚集列存储索引定义支持使用筛选的条件。 若要尽量减少在 OLTP 表中添加列存储索引的性能影响，请使用筛选条件，以便创建仅关于运行工作负荷冷数据的非聚集列存储索引。

-   一个内存中表可以有一个列存储索引。 你可以在创建表时创建它，也可以稍后使用 [ALTER TABLE (Transact-SQL)](../t-sql/statements/alter-table-transact-sql.md) 来添加。 在低于 SQL Server 2016 的版本中，仅基于磁盘的表可以有列存储索引。

有关详细信息，请参阅[列存储索引 - 查询性能](../relational-databases/indexes/columnstore-indexes-query-performance.md)。

**设计指南**


-   一个行存储表可以有一个可更新的非聚集列存储索引。 在低于 SQL Server 2014 的版本中，非聚集列存储索引是只读的。



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-spexecuteexternalscript-transact-sqlsystem-stored-proceduressp-execute-external-script-transact-sqlmd"></a>8. &nbsp; [sp_execute_external_script (Transact-SQL)](system-stored-procedures/sp-execute-external-script-transact-sql.md)

更新日期：2018-01-23 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_7) | [下一篇](#TitleNum_9)）

<!-- Source markdown line 207.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0ee4d591ae9d9a5c015eec98aad9ccbb86268761 ac9b439c23ffae5fcc77639de6ff955763cf5844  (PR=4696  ,  Filename=sp-execute-external-script-transact-sql.md  ,  Dirpath=docs\relational-databases\system-stored-procedures\  ,  MergeCommitSha40=d7dcbcebbf416298f838a39dd5de6a46ca9f77aa) -->



要生成使用 Python 的类似模型，需要将语言标识符从 `@language=N'R'` 更改为 `@language = N'Python'`，并对 `@script` 参数进行必要的修改。 否则，所有参数均与 R 在功能上相同。

**C.创建 Python 模型并通过该模型生成分数**


本示例演示了如何使用 sp\_execute\_external\_ 在 Python 模型中生成分数。

```
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

**Input query to generate the customer data**

DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders`

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

**Get data from input query**

customer_data = my_input_data

**Define the model**

n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

Python 代码中使用的列标题不是对 SQL Server 的输出；因此，使用 WITH RESULTS 语句来为 SQL 指定要使用的列名称和数据类型。

要进行评分，还可以使用本机 [PREDICT](system-stored-procedures/../../t-sql/queries/predict-transact-sql.md) 函数，此函数无需调用 Python 或 R 运行时，因此更加快速。




&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-create-primary-keystablescreate-primary-keysmd"></a>9.&nbsp; [创建主键](tables/create-primary-keys.md)

更新日期：2018-01-18 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  （[上一篇](#TitleNum_8)）

<!-- Source markdown line 102.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d18b485f314cc005d624cab8a51650d3b8f55f89 9bd2e9453206e8940d30b0a01c43f9d8e1aed606  (PR=4652  ,  Filename=create-primary-keys.md  ,  Dirpath=docs\relational-databases\tables\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



**在新表中创建具有非聚集索引的主键**


1.  在“对象资源管理器”中，连接到数据库引擎实例。

2.  在标准菜单栏上，单击 **“新建查询”**。

3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例创建一个表并针对 `CustomerID`列定义一个主键，针对 `TransactionID` 定义一个群集索引。

```
    USE AdventureWorks2012;
    GO
    CREATE TABLE Production.TransactionHistoryArchive1
    (
       CustomerID uniqueidentifier DEFAULT NEWSEQUENTIALID(),
       TransactionID int IDENTITY (1,1) NOT NULL,
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY NONCLUSTERED (uniqueidentifier)
    );
    GO

    -- Now add the clustered index
    CREATE CLUSTERED INDEX CIX_TransactionID ON Production.TransactionHistoryArchive1 (TransactionID);
    GO
```







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


