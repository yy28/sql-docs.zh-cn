---
title: "全文搜索入门 | Microsoft Docs"
ms.date: "08/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "全文目录 [SQL Server], 创建"
  - "全文索引 [SQL Server], 创建"
  - "全文搜索 [SQL Server], 关于"
  - "全文搜索 [SQL Server], 设置"
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
caps.latest.revision: 76
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 72
---
# 全文搜索入门
全文搜索通过使用以下“语言组件”支持多种语言：断字符和词干分析器、包含非索引字（也称为“干扰词”）的非索引字表及同义词库文件。 在某些情况下，同义词库文件和非索引字表需要由数据库管理员配置。 给定同义词库文件支持使用相应语言的所有全文索引，给定非索引字表可以根据您的需要与尽可能多的全文索引相关联。  
 
SQL Server 数据库默认启用全文模式，但必须先[创建全文目录](https://msdn.microsoft.com/library/bb326035.aspx)，然后在要搜索的表或索引视图上创建全文索引。
 
 ## 分步说明 
 
 如果希望获取分步说明，请转到[使用全文索引向导](https://msdn.microsoft.com/library/ms180091.aspx)主题。

本主题涵盖注意事项、示例和其他主题的链接。
##  <a name="configure"></a> 规划设置

为启用全文搜索，有两个基本步骤用以在数据库中配置表列：  
  
- 创建全文目录。  
  
- 在要搜索的表或索引视图上创建全文索引。 

     全文索引是一种特殊类型的基于标记的功能性索引，由全文引擎生成和维护。 若要对表或视图创建全文搜索，则该表或视图必须具有唯一的、不可为 Null 的单列索引。 全文引擎需要使用此唯一索引将表中的每一行映射到一个唯一的可压缩键。 一个全文索引可包括以下列：**char**、**varchar**、**nchar**、**nvarchar**、**text**、**ntext**、**image**、**xml**、**varbinary** 和 **varbinary(max)**。 有关详细信息，请参阅[创建和管理全文索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)。   
  
     每个全文索引必须属于一个全文目录。 您可以为每个全文索引创建一个单独的文本目录，也可以将多个全文索引与给定目录关联起来。 全文目录是虚拟对象，不属于任何文件组。 该目录是表示一组全文索引的逻辑概念。  
  

 全文索引和普通 SQL Server 索引之间的区别：  
  
|全文索引|普通 SQL Server 索引|  
|------------------------|--------------------------------|  
|每个表只允许有一个全文索引。|每个表允许有多个普通索引。|  
|将数据添加到全文索引的操作称为“填充”，可以通过计划或特定请求来请求填充，也可以在添加新数据时自动填充。|当插入、更新或删除作为其基础的数据时自动更新。|  
|在同一个数据库内分组为一个或多个全文目录。|不分组。|  
    
##  <a name="options"></a> 选项  
  
### 列语言  
 有关选择列语言的信息，请参阅[创建全文索引时选择语言](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)。  
  
### 选择全文索引的文件组  
 生成全文索引是一个需要大量占用 I/O 的过程（它需要频繁地从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 读取数据，然后将筛选后的数据传播到全文索引）。 最佳做法是将全文索引置于最适于最大程度地提高 I/O 性能的数据库文件组中，或者将全文索引置于另一个卷的其他文件组中。  
  
 建议将表数据和任何附属全文目录存储在同一个文件组中。 出于性能的考虑，有时可能需要将表数据和全文索引置于存储在不同卷上的不同文件组中，以便最大化 I/O 并行度。  

  
### 分配全文索引   
 
 建议将具有相同更新特征的表（如更改次数少的与更改次数多的，或者在一天中某个特定时段内频繁更改的表）关联在一起，并置于同一全文目录下。 通过设置全文目录填充计划，会使全文索引与表保持同步，且在数据库活动较多时不会对数据库服务器的资源使用产生负面影响。  
  
 请考虑以下原则：  
  
-   始终选择可用于全文唯一键的最小唯一索引。 （最好是 4 个字节、基于整数的索引。）这将显著减少文件系统中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search 服务所需要的资源。 如果主键较大（超过 100 个字节），可以考虑选择表中的另一个唯一索引（或创建另一个唯一索引）来作为全文唯一键。 否则，如果全文唯一键的大小超过所允许的最大值（900 个字节），全文填充将无法继续进行。  
  
-   如果创建索引的表有数百万行，请将该表分配到其自身的全文目录。  
  
-   考虑要进行全文索引的表中发生的更改量以及总行数。 如果要更改的总行数与上次全文填充期间表中出现的行数合起来达到了数百万行，请将该表分配到其自身的全文目录。  

  
### 关联非索引字表   
  “非索引字表”  是非索引字（也称为“干扰词”）的列表。 非索引字表与每个全文索引相关联，因而该非索引字表中的词会应用于对该索引的全文查询。 默认情况下，系统非索引字表与新的全文索引相关联。 也可以创建和使用你自己的非索引字表。 有关详细信息，请参阅[为全文搜索配置和管理非索引字和非索引字表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
 例如，下面的 [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句可通过从系统非索引字表进行复制来创建名为 myStoplist3 的新全文非索引字表：  
  
```  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 下面的 [ALTER FULLTEXT STOPLIST](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句可更改名为 myStoplist 的非索引字表，首先为西班牙语添加词“en”，再为法语添加词“en”：  
  
```  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
    
## 更新索引  
 与普通 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 索引一样，全文索引可以在相关表中的数据修改时自动更新。 这是默认行为。 另外，还可以手动或在预定的间隔更新全文索引。 由于填充全文索引可能极为耗费时间和资源，因此索引更新通常作为异步进程执行，该进程在后台运行，在基表中进行修改后使全文索引保持最新。 
 
 在基表中进行每次更改后立即更新全文索引可能会占用大量的资源。 因此，如果更新/插入/删除操作非常频繁，您可能会发现查询性能有所降低。 如果出现这种情况，可以考虑制定一个手动的更改跟踪更新计划，以便按一定的间隔更新大量的更改，从而避免与查询争用资源。  
  
 通过使用 FULLTEXTCATALOGPROPERTY 或 OBJECTPROPERTYEX 函数监视填充状态。 若要获得目录填充状态，请运行以下语句：  
  
```  
SELECT FULLTEXTCATALOGPROPERTY('AdvWksDocFTCat', 'Populatestatus');  
```  
  
 通常，如果正在进行完全填充，则返回的结果为 1。  
 

##  <a name="example"></a> 示例：设置全文搜索  
 下面的示例由两部分组成，首先对 AdventureWorks 数据库创建名为 `AdvWksDocFTCat` 的全文目录，然后对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中的 `Document` 表创建全文索引。 此语句将在安装过程中指定的默认位置创建全文目录。 将在默认目录下创建名为 `AdvWksDocFTCat` 的文件夹。  
  
1.  为了创建名为 `AdvWksDocFTCat` 的全文目录，此示例使用了 [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md) 语句：  
  
    ```  
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
  
2.  在对 Document 表创建全文索引之前，请确保该表具有唯一的、不可为 Null 的单列索引。 下面的 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) 语句可对 Document 表的 DocumentID 列创建唯一索引 `ui_ukDoc`：  
  
    ```  
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  
  
3.  具有唯一键后，即可使用下面的 [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) 语句对 `Document` 表创建全文索引。  
  
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
  
     此示例中定义的 TYPE COLUMN 指定表中的类型列，该列包含“Document”列（为二进制类型）的每一行中文档的类型。 此类型列存储给定行中文档的、由用户提供的文件扩展名 —“.doc”、“.xls”等等。 全文引擎使用给定行中的文件扩展名调用正确的筛选器，以用于分析该行中的数据。 在该筛选器对该行的二进制数据进行分析后，指定的断字符将分析其内容（在此示例中，使用的是英国英语的断字符）。 请注意，仅在进行索引时，或者在对全文索引启用了自动更改跟踪的情况下用户在基表中插入或更新列时，才会执行筛选过程。 有关详细信息，请参阅[配置和管理搜索筛选器](../../relational-databases/search/configure-and-manage-filters-for-search.md)。  
  
   
## 创建全文目录  
  
-   [CREATE FULLTEXT CATALOG (Transact-SQL)](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)  
  
-   [创建和管理全文索引目录](../../relational-databases/search/create-and-manage-full-text-catalogs.md)  
  
## 查看索引  
  
-   [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
## 创建唯一索引  
  
-   [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)  
  
-   [打开表设计器 (Visual Database Tools)](../../ssms/visual-db-tools/open-table-designer-visual-database-tools.md)  
  
## 创建全文索引  
  
-   [CREATE FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
-   [创建和管理全文索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)  
  
## 查看有关全文索引的信息  
  
|目录视图或动态管理视图|说明|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)|对于全文索引引用的每个全文目录，返回与其对应的一行。|  
|[sys.fulltext_index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)|对构成全文索引的每列都包含一行。|  
|[sys.fulltext_index_fragments (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)|全文索引使用内部表（称为“全文索引片断”）来存储倒排索引数据。 可以使用此视图来查询有关这些片断的元数据。 在此视图中，每个全文索引片断在每个包含全文索引的表中各占一行。|  
|[sys.fulltext_indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)|表对象的每个全文索引各占一行。|  
|[sys.dm_fts_index_keywords (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)|返回有关指定表的全文索引内容的信息。|  
|[sys.dm_fts_index_keywords_by_document (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)|返回有关指定表的文档级全文索引内容的信息。 给定关键字可以出现在几个文档中。|  
|[sys.dm_fts_index_population (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)|返回有关当前正在进行的全文索引填充的信息。|  
  

  
## 详细信息 
 [CREATE FULLTEXT CATALOG (Transact-SQL)](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT STOPLIST (Transact-SQL)](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [填充全文索引](../../relational-databases/search/populate-full-text-indexes.md)   
 [FULLTEXTCATALOGPROPERTY (Transact-SQL)](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [OBJECTPROPERTYEX (Transact-SQL)](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  