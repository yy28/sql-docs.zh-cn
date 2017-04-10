---
title: "发布数据和数据库对象 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "用户定义类型 [SQL Server 复制]"
  - "项目 [SQL Server 复制], 删除"
  - "对象 [SQL Server 复制]"
  - "发布 [SQL Server 复制], 创建"
  - "合并复制 [SQL Server 复制]，发布"
  - "仅限于架构的项目 [SQL Server 复制]"
  - "发布 [SQL Server 复制]，数据库对象"
  - "项目 [SQL Server 复制], 定义"
  - "发布 [SQL Server 复制]，功能"
  - "复制 [SQL Server]，发布"
  - "发布 [SQL Server 复制]，视图"
  - "表 [SQL Server 复制]"
  - "架构 [SQL Server 复制]"
  - "发布 [SQL Server 复制]，数据"
  - "架构 [SQL Server 复制]，发布"
  - "项目 [SQL Server 复制]，存储过程和"
  - "发布 [SQL Server 复制]，表"
  - "别名数据类型 [SQL Server 复制]"
  - "发布 [SQL Server 复制], 删除"
  - "快照复制 [SQL Server]，发布"
  - "项目 [SQL Server 复制], 修改"
  - "事务复制，发布"
  - "发布 [SQL Server 复制]，存储过程"
  - "发布 [SQL Server 复制]"
  - "视图 [SQL Server 复制]"
  - "存储过程 [SQL Server 复制]，发布"
  - "发布 [SQL Server 复制]，架构选项"
  - "项目 [SQL Server 复制], 添加"
  - "发布 [SQL Server 复制], 修改"
  - "用户定义函数 [SQL Server 复制]"
ms.assetid: d986032c-3387-4de1-a435-3ec5e82185a2
caps.latest.revision: 83
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 83
---
# 发布数据和数据库对象
  创建发布时，可以选择希望发布的表和其他数据库对象。 您可以使用复制来发布下列数据库对象。  
  
|数据库对象|快照复制和事务复制|合并复制|  
|---------------------|--------------------------------------------------------|-----------------------|  
|表|X|X|  
|已分区表|X|X|  
|存储过程 - 定义（[!INCLUDE[tsql](../../../includes/tsql-md.md)] 和 CLR）|X|X|  
|存储过程 - 执行（[!INCLUDE[tsql](../../../includes/tsql-md.md)] 和 CLR）|X|否|  
|视图|X|X|  
|索引视图|X|X|  
|作为表的索引视图|X|否|  
|用户定义类型 (CLR)|X|X|  
|用户定义函数（[!INCLUDE[tsql](../../../includes/tsql-md.md)] 和 CLR）|X|X|  
|别名数据类型|X|X|  
|全文检索|X|X|  
|架构对象（约束、索引、用户 DML 触发器、扩展属性和排序规则）|X|X|  
  
## 创建发布  
 若要创建发布，请提供下列信息：  
  
-   分发服务器。  
  
-   快照文件的位置。  
  
-   发布数据库。  
  
-   要创建的发布的类型（快照发布、事务发布、具有可更新订阅的事务发布或合并发布）。  
  
-   包含在发布中的数据和数据库对象（项目）。  
  
-   用于所有发布类型的静态行筛选器和列筛选器，以及用于合并发布的参数化行筛选器和联接筛选器。  
  
-   快照代理计划。  
  
-   运行下列代理时使用的帐户：所有发布的快照代理；所有事务发布的日志读取器代理；允许更新订阅的事务发布的队列读取器代理。  
  
-   发布的名称和说明。  
  
 有关如何使用发布的信息，请参阅下列主题：  
  
-   [创建发布](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [定义项目](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [查看和修改项目属性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [删除发布](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [删除项目](../../../relational-databases/replication/publish/delete-an-article.md)  
  
> [!NOTE]  
>  删除项目或发布并不能从订阅服务器中删除对象。  
  
## 发布表  
 最经常发布的对象就是表。 下列链接提供其他与发布表有关的区域的信息：  
  
-   [筛选已发布数据](../../../relational-databases/replication/publish/filter-published-data.md)  
  
-   [事务复制的项目选项](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
-   [合并复制的项目选项](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  
  
-   [复制标识列](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
 为复制发布表时，可以指定应将哪些架构对象复制到订阅服务器。例如，已声明的引用完整性（主键约束、引用约束和唯一约束）、索引、用户 DML 触发器（不能复制的 DDL 触发器）、扩展属性和排序规则。 仅在发布服务器和订阅服务器之间的初始同步中复制扩展属性。 如果在初始同步之后添加或修改扩展属性，则不会复制该更改。  
  
 若要指定架构选项，请参阅 [指定架构选项](../../../relational-databases/replication/publish/specify-schema-options.md) 或 <xref:Microsoft.SqlServer.Replication.Article.SchemaOption%2A>。  
  
### 已分区表和已分区索引  
 复制支持发布已分区表和已分区索引。 支持级别取决于使用的复制类型，以及您为发布指定的选项以及与已分区表相关联的项目。 有关详细信息，请参阅 [复制已分区表和索引](../../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。  
  
## 发布存储过程  
 所有类型的复制都允许复制存储过程定义：CREATE PROCEDURE 将复制到每个订阅服务器。 如果是公共语言运行时 (CLR) 存储过程，则相关联的程序集也要复制。 对过程的更改将复制到订阅服务器。关联程序集的更改则不然。  
  
 除了复制存储过程的定义，通过事务复制还可以复制存储过程的执行。 这对于复制面向维护的存储过程的结果很有用处，这种存储过程的结果会影响大量的数据。 有关详细信息，请参阅 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
## 发布视图  
 各种类型的复制都允许复制视图。 可以将视图（若是索引视图，要连同其所附索引）复制到订阅服务器，同时还必须复制基表。  
  
 对于索引视图，事务复制还允许将其作为表而非视图进行复制，这样就无需再复制基表。 若要执行此操作，指定"indexed 的 view logbased"选项之一 *@type* 参数 [sp_addarticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 有关使用 **sp_addarticle**, ，请参阅 [定义项目](../../../relational-databases/replication/publish/define-an-article.md)。  
  
## 发布用户定义函数  
 将 CLR 函数和 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 函数的 CREATE FUNCTION 语句复制到每个订阅服务器。 对于 CLR 函数，还要复制关联程序集。 函数的更改将复制到订阅服务器，关联程序集的更改则不然。  
  
## 发布用户定义类型和别名数据类型  
 与其他列一样，把使用用户定义类型或别名数据类型的列复制到订阅服务器。 创建表之前，将在订阅服务器上执行的每个复制类型的创建 TYPEstatement。 对于用户定义类型，还要将关联程序集复制到每个订阅服务器。 用户定义类型和别名数据类型的更改不复制到订阅服务器。  
  
 如果在数据库中定义一个类型，但在创建发布时任何列都不引用该类型，则不将该类型复制到订阅服务器。 如果以后要在该数据库中创建这种类型的列并想复制该列，就必须先将该类型（对于用户定义的类型还要连同关联程序集）手动复制到每个订阅服务器。  
  
## 发布全文检索  
 将 CREATE FULLTEXT INDEX 语句复制到每个订阅服务器，并在订阅服务器上创建全文索引。 不会复制使用 ALTER FULLTEXT INDEX 对全文检索所做的更改。  
  
## 对发布的对象进行架构更改  
 复制支持对已发布对象进行多种架构更改。 对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 发布服务器中相应的发布对象进行下列任何一种架构更改时，默认情况下会将该更改传播到所有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器：  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 有关详细信息，请参阅 [发布数据库上进行架构更改](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
## 有关发布的注意事项  
 发布数据库对象时要注意下列问题：  
  
-   在创建发布和初始快照的过程中，用户可以访问数据库，但建议在发布服务器中活动较少时创建发布。  
  
-   如果已在数据库中创建了发布，则不能重命名该数据库。 若要对其重命名，必须首先删除数据库中的复制。  
  
-   如果发布的数据库对象依赖于一个或多个其他数据库对象，则必须发布所有被引用对象。 例如，如果要发布的视图依赖于一个表，则也必须发布该表。  
  
    > [!NOTE]  
    >  如果将项目添加到合并发布，但现有的项目依赖于新项目，则必须指定使用这两篇文章的处理顺序 **@processing_order** 参数 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 和 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 请考虑以下情况：您要发布一个表，但不发布该表引用的函数。 如果不发布该函数，则无法在订阅服务器中创建相应的表。 在将该函数添加到发布︰ 将值指定为 **1** 为 **@processing_order** 参数 **sp_addmergearticle**; 并在指定的值 **2** 为 **@processing_order** 参数 **sp_changemergearticle**, ，该参数将表名指定 **@article**。 此处理顺序可确保在创建依赖于某函数的表之前在订阅服务器上创建该函数。 每个项目可以使用不同的数字，只要函数的数字小于表的数字即可。  
  
-   发布名称中不能包含以下字符：% * [ ] | : " ? \ / \< >。  
  
### 对发布对象的限制  
  
-   可以发布的最大项目数和列数因发布类型而异。 有关详细信息，请参阅的"复制对象"一节 [适用于 SQL Server 的最大容量规范](../../../sql-server/maximum-capacity-specifications-for-sql-server.md)。  
  
-   定义为 WITH ENCRYPTION 的存储过程、视图、触发器和用户定义函数不能作为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 复制的一部分发布。  
  
-   XML 架构集合可以复制，但初始快照之后的更改则不复制。  
  
-   为事务复制发布的表必须有一个主键。 如果表位于事务复制发布中，则无法禁用任何与主键列关联的索引。 复制需要使用这些索引。 若要禁用索引，必须先从发布中删除该表。  
  
-   绑定默认值创建与 [sp_bindefault & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md) 不复制 （绑定默认值以使用 ALTER TABLE 或 CREATE TABLE 的 DEFAULT 关键字创建的默认设置支持不推荐使用）。  
  
-   由于分发代理传递它们时所采用的顺序，包含针对索引视图的 **NOEXPAND** 提示的函数不能在与引用的表和索引视图相同的发布中发布。 若要解决此问题，请将创建的表和索引视图放置于第一个发布中，并且将包含针对索引视图的 **NOEXPAND** 提示的函数添加到在第一个发布完成后发布的第二个发布中。 或者，创建这些函数的脚本，传递该脚本使用 *@post_snapshot_script* 参数 **sp_addpublication**。  
  
### 架构和对象所有权  
 在新建发布向导中，复制在架构和对象所有权方面具有以下默认行为：  
  
-   对于兼容性级别为 90 或更高的合并发布、快照发布和事务发布中的项目：默认情况下，订阅服务器中的对象所有者与发布服务器中相应对象的所有者相同。 如果订阅服务器中不存在拥有对象的架构，将自动创建这些架构。  
  
-   对于合并发布中兼容级别低于 90 的项目：默认情况下，所有者保留为空，并且在订阅服务器上创建对象的过程中指定为 **dbo** 。  
  
-   对于 Oracle 发布中的项目：默认情况下，所有者指定为 **dbo**。  
  
-   对于使用字符模式快照（用于非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器以及 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 订阅服务器）的发布中的项目：默认情况下，所有者保留为空。 所有者默认为与分发代理或合并代理连接到订阅服务器所使用的帐户关联的所有者。  
  
 可以通过更改对象所有者 **项目属性-\<***文章***>** 对话框和以下存储过程︰ **sp_addarticle**, ，**sp_addmergearticle**, ，**sp_changearticle**, ，和 **sp_changemergearticle**。 有关详细信息，请参阅 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md), ，[定义项目](../../../relational-databases/replication/publish/define-an-article.md), ，和 [查看和修改项目属性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)。  
  
### 将数据发布到运行 SQL Server 早期版本的订阅服务器  
  
-   如果在向运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 早期版本的订阅服务器发布，则复制特定功能和产品整体功能两个方面都会受该版本功能的限制。  
  
-   合并发布使用兼容性级别，它确定哪些功能可以用在发布中，并使您能够支持运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]早期版本的订阅服务器。  
  
### 在多个发布中发布表  
 复制支持按照下列限制在多个发布中发布项目（包括重新发布数据）：  
  
-   如果在事务发布和合并发布中发布项目，请确保 *@published_in_tran_pub* 为合并项目的属性设置为 TRUE。 有关设置属性的详细信息，请参阅 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md) 和 [查看和修改项目属性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)。  
  
     您还应设置 *@published_in_tran_pub* 如果一篇文章是事务订阅的一部分，并且包含在合并发布的属性。 如果是这种情况，注意，默认情况下事务复制期望表在订阅服务器中被视为只读表；如果合并复制对事务订阅中的表进行数据更改，则无法实现数据收敛。 为了避免这种情况，建议您在合并发布中将所有此类表都指定为仅供下载。 这样可以防止合并订阅服务器向表中上载数据更改。 有关详细信息，请参阅 [对 Download-Only 项目优化合并复制性能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
-   不能在合并发布和事务发布中同时发布带有排队更新订阅的项目。  
  
-   支持更新订阅的事务发布所包括的项目不能重新发布。  
  
-   如果在多个支持排队更新订阅的事务发布中发布项目，那么对于所有发布中的项目，下列属性必须具有相同值：  
  
    |属性|sp_addarticle 中的参数|  
    |--------------|---------------------------------|  
    |标识范围管理|**@auto_identity_range** （已弃用） 和 **@identityrangemangementoption**|  
    |发布服务器标识范围|**@pub_identity_range**|  
    |标识范围|**@identity_range**|  
    |标识范围阈值|**@threshold**|  
  
     有关这些参数的详细信息，请参阅 [sp_addarticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。  
  
-   如果在多个合并发布中发布项目，那么对于所有发布中的项目，下列属性必须具有相同值：  
  
    |属性|sp_addmergearticle 中的参数|  
    |--------------|--------------------------------------|  
    |列跟踪|**@column_tracking**|  
    |架构选项|**@schema_option**|  
    |列筛选|**@vertical_partition**|  
    |订阅服务器中载选项|**@subscriber_upload_options**|  
    |条件性删除跟踪|**@delete_tracking**|  
    |错误补偿|**@compensate_for_errors**|  
    |标识范围管理|**@auto_identity_range** （已弃用） 和 **@identityrangemangementoption**|  
    |发布服务器标识范围|**@pub_identity_range**|  
    |标识范围|**@identity_range**|  
    |标识范围阈值|**@threshold**|  
    |分区选项|**@partition_options**|  
    |Blob 列流|**@stream_blob_columns**|  
    |筛选器类型|**@filter_type** (中的参数 **sp_addmergefilter**)|  
  
     有关这些参数的详细信息，请参阅 [sp_addmergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 和 [sp_addmergefilter & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)。  
  
-   事务复制和未筛选的合并复制支持在多个发布中发布表，然后在订阅数据库中的单个表内进行订阅（通常称为“汇总方案”）。 汇总常用于在中央订阅服务器中的一个表中聚合来自多个位置的数据子集。 已筛选的合并发布不支持中央订阅服务器方案。 对于合并复制，通常通过带有参数化行筛选器的单个发布实现汇总。 有关详细信息，请参阅 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
## 另请参阅  
 [向现有发布添加项目和从中删除项目](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [配置分发](../../../relational-databases/replication/configure-distribution.md)   
 [初始化订阅](../../../relational-databases/replication/initialize-a-subscription.md)   
 [编写复制脚本](../../../relational-databases/replication/scripting-replication.md)   
 [保护发布服务器的安全](../../../relational-databases/replication/security/secure-the-publisher.md)   
 [订阅发布](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  