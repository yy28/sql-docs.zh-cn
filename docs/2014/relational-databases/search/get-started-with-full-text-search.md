---
title: 全文搜索入门 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b6dc03709ea16fb718ff93ed60f75ad4d1515eaf
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52541389"
---
# <a name="get-started-with-full-text-search"></a>全文搜索入门
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的数据库在默认情况下支持全文索引。 不过，若要对表使用全文索引，必须对要使用全文引擎访问的表列设置全文索引功能。  
  
##  <a name="configure"></a> 为全文搜索配置数据库  
 对于任何应用场景，数据库管理员都要执行以下基本步骤来将数据库中的表列配置为可以进行全文搜索：  
  
1.  创建全文目录。  
  
2.  在要搜索的每个表中，按以下方法创建全文索引：  
  
    1.  标识要包含在全文索引中的各个文本列。  
  
    2.  如果给定的列包含存储为二进制数据的文档 (`varbinary(max)`，或`image`数据)，必须指定一个表列 (*类型列*) 以标识被索引的列中每个文档的类型。  
  
    3.  指定对列中文档进行全文搜索时所使用的语言。  
  
    4.  选择全文索引中要使用的更改跟踪机制，以跟踪基表及其列中的更改。  
  
 全文搜索通过使用以下“语言组件”支持多种语言：断字符和词干分析器、包含非索引字（也称为“干扰词”）的非索引字表及同义词库文件。 在某些情况下，同义词库文件和非索引字表需要由数据库管理员配置。 给定同义词库文件支持使用相应语言的所有全文索引，给定非索引字表可以根据您的需要与尽可能多的全文索引相关联。  
  
##  <a name="setup"></a> 设置全文目录和索引  
 这涉及以下基本步骤：  
  
1.  创建全文目录来存储全文索引。  
  
     每个全文索引必须属于一个全文目录。 您可以为每个全文索引创建一个单独的文本目录，也可以将多个全文索引与给定目录关联起来。 全文目录是虚拟对象，不属于任何文件组。 该目录是表示一组全文索引的逻辑概念。  
  
2.  对表或索引视图创建全文索引。  
  
     全文索引是一种特殊类型的基于标记的功能性索引，由全文引擎生成和维护。 若要对表或视图创建全文搜索，则该表或视图必须具有唯一的、不可为 Null 的单列索引。 全文引擎需要使用此唯一索引将表中的每一行映射到一个唯一的可压缩键。 全文索引可以包括 `char`、`varchar`、`nchar`、`nvarchar`、`text`、`ntext`、`image`、`xml`、`varbinary` 和 `varbinary(max)` 列。 有关详细信息，请参阅 [创建和管理全文索引](create-and-manage-full-text-indexes.md)。  
  
 在了解如何创建全文索引之前，请务必考虑它们与普通 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 索引的不同之处。 下表列出了这些差异。  
  
|全文索引|普通 SQL Server 索引|  
|------------------------|--------------------------------|  
|每个表只允许有一个全文索引。|每个表允许有多个普通索引。|  
|将数据添加到全文索引的操作称为“填充”，可以通过计划或特定请求来请求填充，也可以在添加新数据时自动填充。|当插入、更新或删除作为其基础的数据时自动更新。|  
|在同一个数据库内分组为一个或多个全文目录。|不分组。|  
  
  
##  <a name="options"></a> 选择全文索引的选项  
 本节涵盖以下内容：  
  
-   选择列语言  
  
-   选择全文索引的文件组  
  
-   将全文索引分配到全文目录  
  
-   将非索引字表与全文索引关联  
  
-   更新全文索引  
  
### <a name="choosing-the-column-language"></a>选择列语言  
 有关在选择列语言时要注意的事项的信息，请参阅[创建全文索引时选择语言](choose-a-language-when-creating-a-full-text-index.md)。  
  
### <a name="choosing-a-filegroup-for-a-full-text-index"></a>选择全文索引的文件组  
 生成全文索引是一个需要大量占用 I/O 的过程（它需要频繁地从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 读取数据，然后将筛选后的数据传播到全文索引）。 最佳做法是将全文索引置于最适于最大程度地提高 I/O 性能的数据库文件组中，或者将全文索引置于另一个卷的其他文件组中。  
  
 如果您非常注重管理的方便性，建议您将表数据和所有关联的全文目录存储在同一文件组中。 出于性能的考虑，有时您可能需要将表数据和全文索引置于存储在不同卷上的不同文件组中，以便最大化 I/O 并行度。  
  
  
### <a name="assigning-the-full-text-index-to-a-full-text-catalog"></a>将全文索引分配到全文目录  
 计划表的全文索引在全文目录中的位置非常重要。  
  
 建议将具有相同更新特征的表（如更改次数少的与更改次数多的，或者在一天中某个特定时段内频繁更改的表）关联在一起，并置于同一全文目录下。 通过设置全文目录填充计划，会使全文索引与表保持同步，且在数据库活动较多时不会对数据库服务器的资源使用产生负面影响。  
  
 将表分配到全文目录时，应考虑下列准则：  
  
-   始终选择可用于全文唯一键的最小唯一索引。 （最好是 4 个字节、基于整数的索引。）这将显著减少文件系统中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search 服务所需要的资源。 如果主键较大（超过 100 个字节），可以考虑选择表中的另一个唯一索引（或创建另一个唯一索引）来作为全文唯一键。 否则，如果全文唯一键的大小超过所允许的最大值（900 个字节），全文填充将无法继续进行。  
  
-   如果创建索引的表有数百万行，请将该表分配到其自身的全文目录。  
  
-   考虑要进行全文索引的表中发生的更改量以及总行数。 如果要更改的总行数与上次全文填充期间表中出现的行数合起来达到了数百万行，请将该表分配到其自身的全文目录。  
  
  
### <a name="associating-a-stoplist-with-the-full-text-index"></a>将非索引字表与全文索引关联  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 引入了非索引字表。 “非索引字表”  是非索引字（也称为“干扰词”）的列表。 非索引字表与每个全文索引相关联，因而该非索引字表中的词会应用于对该索引的全文查询。 默认情况下，系统非索引字表与新的全文索引相关联。 不过，您也可以创建和使用您自己的非索引字表。 有关详细信息，请参阅 [为全文搜索配置和管理非索引字和非索引字表](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
 例如，以下[CREATE FULLTEXT STOPLIST](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)]语句创建新全文非索引字表通过从系统非索引字表复制名为 myStoplist3:  
  
```  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 下面的 [ALTER FULLTEXT STOPLIST](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句可更改名为 myStoplist 的非索引字表，首先为西班牙语添加词“en”，再为法语添加词“en”：  
  
```  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
  
  
### <a name="updating-a-full-text-index"></a>更新全文索引  
 与普通 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 索引一样，全文索引可以在相关表中的数据修改时自动更新。 这是默认行为。 另外，还可以手动或在预定的间隔更新全文索引。 由于填充全文索引可能极为耗费时间和资源，因此索引更新通常作为异步进程执行，该进程在后台运行，在基表中进行修改后使全文索引保持最新。 在基表中进行每次更改后立即更新全文索引可能会占用大量的资源。 因此，如果更新/插入/删除操作非常频繁，您可能会发现查询性能有所降低。 如果出现这种情况，可以考虑制定一个手动的更改跟踪更新计划，以便按一定的间隔更新大量的更改，从而避免与查询争用资源。  
  
 若要监视填充状态，请使用 FULLTEXTCATALOGPROPERTY 或 OBJECTPROPERTYEX 函数。 若要获得目录填充状态，请运行以下语句：  
  
```  
SELECT FULLTEXTCATALOGPROPERTY('AdvWksDocFTCat', 'Populatestatus');  
```  
  
 通常，如果正在进行完全填充，则返回的结果为 1。  
  
  
##  <a name="example"></a> 示例：设置全文搜索  
 下面的示例由两部分组成，首先对 AdventureWorks 数据库创建名为 `AdvWksDocFTCat` 的全文目录，然后对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中的 `Document` 表创建全文索引。 此语句将在安装过程中指定的默认位置创建全文目录。 将在默认目录下创建名为 `AdvWksDocFTCat` 的文件夹。  
  
1.  为了创建名为 `AdvWksDocFTCat` 的全文目录，此示例使用了 [CREATE FULLTEXT CATALOG](/sql/t-sql/statements/create-fulltext-catalog-transact-sql) 语句：  
  
    ```  
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
  
2.  在对 Document 表创建全文索引之前，请确保该表具有唯一的、不可为 Null 的单列索引。 下面的 [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) 语句可对 Document 表的 DocumentID 列创建唯一索引 `ui_ukDoc`：  
  
    ```  
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  
  
3.  具有唯一键后，即可使用下面的 `Document` CREATE FULLTEXT INDEX [语句对](/sql/t-sql/statements/create-fulltext-index-transact-sql) 表创建全文索引。  
  
    ```  
    CREATE FULLTEXT INDEX ON Production.Document  
    (  
        Document                         --Full-text index column name   
            TYPE COLUMN FileExtension    --Name of column that contains file type information  
            Language 2057                 --2057 is the LCID for British English  
    )  
    KEY INDEX ui_ukDoc ON AdvWksDocFTCat --Unique index  
    WITH CHANGE_TRACKING AUTO            --Population type;  
    GO  
  
    ```  
  
     此示例中定义的 TYPE COLUMN 指定表中的类型列，该列包含“Document”列（为二进制类型）的每一行中文档的类型。 此类型列存储给定行中的用户提供的文件扩展名-".doc"、".xls"和等的文档。 全文引擎使用给定行中的文件扩展名调用正确的筛选器，以用于分析该行中的数据。 在该筛选器对该行的二进制数据进行分析后，指定的断字符将分析其内容（在此示例中，使用的是英国英语的断字符）。 请注意，仅在进行索引时，或者在对全文索引启用了自动更改跟踪的情况下用户在基表中插入或更新列时，才会执行筛选过程。 有关详细信息，请参阅 [配置和管理搜索筛选器](configure-and-manage-filters-for-search.md)。  
  
  
##  <a name="tasks"></a> 常见任务  
  
### <a name="to-create-a-full-text-catalog"></a>创建全文目录  
  
-   [CREATE FULLTEXT CATALOG (Transact-SQL)](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)  
  
-   [创建和管理全文索引目录](create-and-manage-full-text-catalogs.md)  
  
### <a name="to-view-the-indexes-of-a-table-or-view"></a>查看表（或视图）的索引  
  
-   [sys.indexes (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)  
  
### <a name="to-create-a-unique-index"></a>创建唯一索引  
  
-   [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql)  
  
-   [打开表设计器 (Visual Database Tools)](../../ssms/visual-db-tools/visual-database-tools.md)  
  
### <a name="to-create-a-full-text-index"></a>创建全文索引  
  
-   [CREATE FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
-   [创建和管理全文索引](create-and-manage-full-text-indexes.md)  
  
### <a name="to-view-information-about-a-full-text-index"></a>查看有关全文索引的信息  
  
|目录视图或动态管理视图|Description|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql)|对于全文索引引用的每个全文目录，返回与其对应的一行。|  
|[sys.fulltext_index_columns (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|对构成全文索引的每列都包含一行。|  
|[sys.fulltext_index_fragments (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql)|全文索引使用内部表（称为“全文索引片断”）来存储倒排索引数据。 可以使用此视图来查询有关这些片断的元数据。 在此视图中，每个全文索引片断在每个包含全文索引的表中各占一行。|  
|[sys.fulltext_indexes (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql)|表对象的每个全文索引各占一行。|  
|[sys.dm_fts_index_keywords (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql)|返回有关指定表的全文索引内容的信息。|  
|[sys.dm_fts_index_keywords_by_document (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql)|返回有关指定表的文档级全文索引内容的信息。 给定关键字可以出现在几个文档中。|  
|[sys.dm_fts_index_population (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|返回有关当前正在进行的全文索引填充的信息。|  
  
  
## <a name="see-also"></a>请参阅  
 [CREATE FULLTEXT CATALOG (Transact-SQL)](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [CREATE FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [CREATE FULLTEXT STOPLIST (Transact-SQL)](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [CREATE TABLE (Transact-SQL)](/sql/t-sql/statements/create-table-transact-sql)   
 [填充全文索引](populate-full-text-indexes.md)   
 [FULLTEXTCATALOGPROPERTY (Transact-SQL)](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)   
 [OBJECTPROPERTYEX (Transact-SQL)](/sql/t-sql/functions/objectproperty-transact-sql)  
  
  
