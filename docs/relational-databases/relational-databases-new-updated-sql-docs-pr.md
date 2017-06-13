---
title: "已更新-关系数据库文档 |Microsoft 文档"
description: "显示有关在最近更改文档，关系数据库的更新内容的代码段。"
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
ms.date: 05/23/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 3ab051a6fd00670139bb1089dcd3f4af76b9ecef
ms.contentlocale: zh-cn
ms.lasthandoff: 05/25/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>新的和最近的更新： 关系数据库文档



几乎每日 Microsoft 及其现有的文章的一些上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文档网站。 这篇文章显示摘录最近已更新的文章。 可能还会列出链接到新的文章。

定期重新运行程序生成这篇文章。 有时摘录可使用不完善格式，或出现 markdown 源文章中的说明。 此处永远不会显示图像。

报告的以下日期范围和主题的新的更新：



- *日期范围的更新：* &nbsp; **自 2017 年 1-05-01** &nbsp;到&nbsp;**自 2017 年 1-05-23**
- *主题区域：* &nbsp; **关系数据库**。




&nbsp;

## <a name="updated-articles-with-excerpts"></a>与摘录更新的文章

此部分显示的摘自从最近出现了大规模更新的文章中收集的更新。

此处显示的摘自其正确的语义上下文的来自分隔。 此外，有时摘录分开环绕在实际的文章中的重要的 markdown 语法。 因此这些摘录适用于一般性指导原则。 摘录仅使你能够知道您的兴趣是否值得花些时间后，单击，访问实际的文章。

有关这些和其他原因，不从这些摘录中，复制代码并不会为确切真实任何文本摘录。 相反，请访问实际的文章。



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-create-a-graph-database-and-run-some-pattern-matching-queries-using-t-sqlgraphssql-graph-samplemd"></a>1.&nbsp;[创建图形数据库并运行一些模式匹配使用 T-SQL 查询](graphs/sql-graph-sample.md)

*Updated: 2017-05-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 68.  ms.author= "shkale".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ff467bf5fcf13592c796836def36e16e34f8cc31 99fcf0399006de16d0ac7cc9057564d307cb981b -->


```
INSERT INTO Person VALUES (1,'John');
INSERT INTO Person VALUES (2,'Mary');
INSERT INTO Person VALUES (3,'Alice');
INSERT INTO Person VALUES (4,'Jacob');
INSERT INTO Person VALUES (5,'Julie');

INSERT INTO Restaurant VALUES (1,'Taco Dell','Bellevue');
INSERT INTO Restaurant VALUES (2,'Ginger and Spice','Seattle');
INSERT INTO Restaurant VALUES (3,'Noodle Land', 'Redmond');

INSERT INTO City VALUES (1,'Bellevue','wa');
INSERT INTO City VALUES (2,'Seattle','wa');
INSERT INTO City VALUES (3,'Redmond','wa');

-- Insert into edge table. While inserting into an edge table, 
-- you need to provide the $node_id from $from_id and $to_id columns.
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 1), 
       (SELECT $node_id FROM Restaurant WHERE id = 1),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 2), 
      (SELECT $node_id FROM Restaurant WHERE id = 2),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 3), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 4), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 5), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);

INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 1),
      (SELECT $node_id FROM City WHERE id = 1));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 2),
      (SELECT $node_id FROM City WHERE id = 2));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 3),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 4),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 5),
      (SELECT $node_id FROM City WHERE id = 1));

INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE id = 1),
      (SELECT $node_id FROM City WHERE id =1));
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sysfngetauditfile-transact-sqlsystem-functionssys-fn-get-audit-file-transact-sqlmd"></a>2. &nbsp; [sys.fn_get_audit_file (TRANSACT-SQL)](system-functions/sys-fn-get-audit-file-transact-sql.md)

*Updated: 2017-05-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1) | [Next](#TitleNum_3))

<!-- Source markdown line 145.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 046fa92ad1b7e6bb7a956493ca06cf72d45b5285 fbf55361da90663835d7e107fda697c358e0e061 -->



- **Azure SQL 数据库**

  此示例从名为 `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel` 的文件读取。  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  此示例将读取从开头的服务器的日志的所有审核`Sh`。  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```





&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-manage-retention-of-historical-data-in-system-versioned-temporal-tablestablesmanage-retention-of-historical-data-in-system-versioned-temporal-tablesmd"></a>3.&nbsp;[管理的系统版本控制临时表中历史数据保留期](tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)

*Updated: 2017-05-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_2))

<!-- Source markdown line 425.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ee69beb6a46913934d4a322f5d95343cc86f2ec4 94da98fec4ab16636a4581c16eb4456e2d1ff66b -->



**使用临时历史记录保持期策略方法**

> **注意：**使用临时历史记录保留策略方法适用于 [！包括 [sqldbesa.../../includes/sqldbesa-md.md)] 和 SQL Server 2017 从 CTP 1.3 开始。  

可以是临时历史记录保持期的单个表级别配置，它允许用户创建灵活期限策略。 应用临时保留，这是简单： 它要求只有一个参数来在表创建或架构更改过程中设置。

在定义保留策略后，Azure SQL 数据库启动定期检查是否启用自动数据清理符合条件的历史行。 标识匹配的行和历史记录表从其删除以透明方式，发生的后台任务来计划和运行系统。 才会检查表示一端的 SYSTEM_TIME 时间段的列上基于的历史记录表行的保留时间条件。 如果保持期内，例如，设置为六个月，适合清除表行满足以下条件：
```
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
```
在前面的示例中，我们已假设 ValidTo 列对应于 SYSTEM_TIME 时间段的末尾。
**如何配置保留策略？**

在配置的临时表的保留策略之前，请首先检查是否在数据库级别启用临时历史记录保持期：
```
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
```
数据库标志**is_temporal_history_retention_enabled**默认情况下，设置为 ON 但用户可以使用 ALTER DATABASE 语句更改它。 它还会自动在时间还原操作点后设置为 OFF。 若要启用你的数据库的临时历史记录保持期清除，请执行以下语句：
```
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
```
通过指定 HISTORY_RETENTION_PERIOD 参数值在表创建期间配置保留策略：
```
CREATE TABLE dbo.WebsiteUserInfo
```





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact 的最近更新的文章的列表

此 compact 列表提供了在上一节中列出的所有更新文章的链接。

1. [创建图形数据库并运行一些模式匹配使用 T-SQL 查询](#TitleNum_1)
2. [sys.fn_get_audit_file (TRANSACT-SQL)](#TitleNum_2)
3. [管理版本由系统控制的临时表中历史数据的保留期](#TitleNum_3)


<a name="sisters2"/>

&nbsp;

## <a name="sister-articles"></a>相关文章

本部分列出了一些相同的 GitHub 存储库中的其他使用者区域中的最近更新项目非常相似文章。


&nbsp;

[Microsoft /**sql 文档 pr** ](https://github.com/microsoftdocs/sql-docs-pr/) GitHub.com 上的存储库：

- [最近更新：**关系数据库和 Microsoft SQL Server**文档](/sql/relational-databases/relational-databases-new-updated-sql-docs-pr)
- [最近更新： **Microsoft SQL Server**文档](/sql/sql-server/sql-server-new-updated-sql-docs-pr)
- [最近更新： **TRANSACT-SQL 在 SQL Server 中**文档](/sql/t-sql/t-sql-new-updated-sql-docs-pr)


&nbsp;

<!--
[Microsoft/**azure-docs**](https://github.com/microsoft/azure-docs/) repository on GitHub.com:

- [Sisters list for **azure-docs** repo](https://docs.microsoft.com/azure/sql-server-new-updated-azure-docs/#sisters2)
-->

&nbsp;



