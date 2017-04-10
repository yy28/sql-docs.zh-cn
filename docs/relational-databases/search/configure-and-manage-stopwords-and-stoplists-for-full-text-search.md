---
title: "为全文搜索配置和管理非索引字和非索引字表 | Microsoft Docs"
ms.custom: ""
ms.date: "02/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "非索引字表 [全文搜索]"
  - "全文搜索 [SQL Server], 非索引字表"
  - "全文搜索 [SQL Server], 干扰词"
  - "干扰词 [全文搜索]"
  - "全文搜索 [SQL Server], 非索引字"
  - "非索引字 [全文搜索]"
ms.assetid: 43b5ce7b-9f09-4443-8a5b-c3da6eb28bcc
caps.latest.revision: 81
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 79
---
# 为全文搜索配置和管理非索引字和非索引字表
  为了精简全文检索，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了一种机制，用于去掉那些经常出现但对搜索无益的字符串。 这些去掉的字符串称为“非索引字” 。 在索引创建期间，全文引擎将忽略全文检索中的非索引字。 也就是说全文查询将不搜索非索引字。  
  
##  <a name="understand"></a> 了解非索引字和非索引字表  
 非索引字可以是在特定语言中具有含义的词，也可以是不具有语言含义的“标记”  。 例如，在英语中，诸如“a”、“and”、“is”和“the”之类的词将被排除在全文检索之外，这是因为已经知道它们对搜索没有用处。  
  
 尽管全文检索会忽略所包含的非索引字，但它确实会考虑非索引字的位置。 例如，请看下面这个短语：“Instructions are applicable to these Adventure Works Cycles models”。 下表显示了短语中各个词的位置：  
  
|Word|位置|  
|----------|--------------|  
|Instructions|1|  
|are|2|  
|applicable|3|  
|实例部署到 Windows Azure 虚拟机 (VM) 中的|4|  
|these|5|  
|Adventure|6|  
|Works|7|  
|Cycles|8|  
|模型|9|  
  
 分别在第 2、第 4 和第 5 个位置的非索引字“are”、“to”和“these”将被排除在全文检索之外。 但是会保留它们的位置信息，从而使短语中其他词的位置不受影响。  
  
 使用称为“非索引字表”的对象在数据库中管理非索引字。 “非索引字表”是一个由非索引字组成的列表，这些非索引字在与全文检索关联时会应用于该索引的全文查询。  
  
 [本主题内容](#TOP)  
  
##  <a name="creating"></a> 创建非索引字表  
 可使用下列任一方法创建非索引字表：  
  
-   在数据库中使用系统提供的非索引字表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为每种支持的语言（即默认情况下与给定断字符关联的每种语言）都附带了一个包含最常用非索引字的系统非索引字表。 系统非索引字表包含所有支持语言的常用非索引字。  可以复制系统非索引字表并通过添加和删除非索引字来自定义自己的非索引字表。  
  
     系统非索引字表安装在 [Resource](../../relational-databases/databases/resource-database.md) 数据库中。  
  
-   创建自己的非索引字表，然后针对您所指定的任何语言将非索引字添加到非索引字表中。 必要时，您还可以从您的非索引字表中删除非索引字。  
  
-   在当前服务器实例中使用任何其他数据库中的现有自定义非索引字表，然后根据需要添加和删除非索引字。  
  
 **创建非索引字表**  
  
-   [CREATE FULLTEXT STOPLIST (Transact-SQL)](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)  
  
#### 在 Management Studio 中创建全文非索引字表  
  
1.  在对象资源管理器中，展开服务器。  
  
2.  展开“数据库”，然后展开要在其中创建全文非索引字表的数据库。  
  
3.  展开“存储”，然后右键单击“全文非索引字表”。  
  
4.  选择“新建全文非索引字表”。  
  
5.  指定非索引字表名称。  
  
6.  （可选）将另外某人指定为非索引字表所有者。  
  
7.  从下列创建非索引字表的选项中选择一个：  
  
    -   **创建空非索引字表**  
  
    -   **从系统非索引字表创建**  
  
    -   **从现有全文非索引字表创建**  
  
     有关详细信息，请参阅[新建全文非索引字表（常规页）](../Topic/New%20Full-Text%20Stoplist%20\(General%20Page\).md)。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 **删除非索引字表**  
  
-   [DROP FULLTEXT STOPLIST (Transact-SQL)](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)  
  
 [本主题内容](#TOP)  
  
##  <a name="queries"></a> 在全文查询中使用非索引字表  
 若要在查询中使用非索引字表，必须将该非索引字表与全文检索关联。 可以在创建全文检索时将非索引字表附加到全文检索中，也可以在以后更改索引来添加非索引字表。  
  
 **创建全文检索并将非索引字表与其关联起来**  
  
-   [CREATE FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
 **将非索引字表与现有的全文检索关联起来或取消它们之间的关联**  
  
-   [ALTER FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
 **取消非索引字导致全文查询的布尔操作失败时产生的错误消息。**  
  
-   [transform noise words 服务器配置选项](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)  
  
 [本主题内容](#TOP)  
  
##  <a name="viewing"></a> 查看非索引字表和非索引字表的元数据  
 **查看非索引字表的所有非索引字**  
  
-   [sys.fulltext_stopwords (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
 **获取有关当前数据库中所有非索引字表的信息**  
  
-   [sys.fulltext_stoplists (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
  
-   [sys.fulltext_stopwords (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
 **查看断字符的词汇切分结果、同义词库和非索引字表组合**  
  
-   [sys.dm_fts_parser (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)  
  
 [本主题内容](#TOP)  
  
##  <a name="change"></a> 在非索引字表中更改非索引字  
 **向非索引字表中添加非索引字或从中删除非索引字**  
  
-   [ALTER FULLTEXT STOPLIST (Transact-SQL)](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)  
  
#### 使用 Management Studio 更改非索引字表中的非索引字  
  
1.  在对象资源管理器中，展开服务器。  
  
2.  展开 **“数据库”**，然后展开数据库。  
  
3.  展开 **“存储”**，然后选择 **“全文非索引字表”**。  
  
4.  右键单击要更改其属性的非索引字表，然后选择“属性”。  
  
5.  在“全文非索引字表属性”[](../Topic/Full-Text%20Stoplist%20Properties.md)对话框中：  
  
    1.  在 **“操作”** 列表框中，选择下列操作之一： **“添加非索引字”**、 **“删除非索引字”**、 **“删除所有非索引字”**或 **“清除非索引字表”**。  
  
    2.  如果对选定的操作启用了 **“非索引字”** 文本框，请输入一个非索引字。 该非索引字必须是唯一的，也就是说，在针对所选语言的此非索引字表中还不存在该非索引字。  
  
    3.  如果对选定的操作启用了“全文语言”列表框，请选择一种语言。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 [本主题内容](#TOP)  
  
##  <a name="upgrade"></a> 从 SQL Server 2005 升级干扰词  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 干扰词已替换为非索引字。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升级数据库后，将不再使用干扰词文件。 然而，干扰词文件存储在 FTDATA\FTNoiseThesaurusBak 文件夹中，您可以在以后更新或生成对应的非索引字表时使用它们。 有关将干扰词文件升级到非索引字表的信息，请参阅[升级全文搜索](../../relational-databases/search/upgrade-full-text-search.md)。  
  
 [本主题内容](#TOP)  
  
  