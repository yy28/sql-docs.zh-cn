---
title: "表 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "表 [SQL Server]"
  - "表组件 [SQL Server]"
ms.assetid: 82d7819c-b801-4309-a849-baa63083e83f
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# 表
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  表是包含数据库中所有数据的数据库对象。 数据在表中的逻辑组织方式与在电子表格中相似，都是按行和列的格式组织的。 每一行代表一条唯一的记录，每一列代表记录中的一个字段。 例如，在包含公司雇员数据的表中，每一行代表一名雇员，各列分别代表该雇员的信息，如雇员编号、姓名、地址、职位以及家庭电话号码等。  
  
-   数据库中的表数仅受数据库中允许的对象数 (2,147,483,647) 的限制。 标准的用户定义的表可以有多达 1024 列。 表的行数仅受服务器的存储容量的限制。  
  
-   您可将属性分配到表和表中的每个列以控制允许的数据和其他属性。 例如，您可在列上创建约束以禁止空值或在未指定值时提供默认值，您也可以在表上指定强制唯一性或定义表之间的关系的键约束。  
  
-   可对表中的数据按行或页进行压缩。 通过数据压缩，可在页上存储更多的行。 有关详细信息，请参阅 [Data Compression](../../relational-databases/data-compression/data-compression.md)。  
  
## 表的类型  
 除了基本用户定义表的标准角色以外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还提供了下列类型的表，这些表在数据库中起着特殊的作用。  
  
 已分区表  
 已分区表是将数据水平划分为多个单元的表，这些单元可以分布到数据库中的多个文件组中。 在维护整个集合的完整性时，使用分区可以快速而有效地访问或管理数据子集，从而使大型表或索引更易于管理。 默认情况下， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持多达 15,000 个分区。 有关详细信息，请参阅 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  
  
 临时表  
 临时表存储在 **tempdb** 中。 临时表有两种类型：本地表和全局表。 它们在名称、可见性以及可用性上有区别。 本地临时表的名称以单个数字符号 (#) 打头；它们仅对当前的用户连接是可见的；当用户从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例断开连接时被删除。 全局临时表的名称以两个数字符号 (##) 打头，创建后对任何用户都是可见的，当所有引用该表的用户从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例断开连接时将被删除。  
  
 系统表  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将定义服务器配置及其所有表的数据存储在一组特殊的表中，这组表称为系统表。 用户不能直接查询或更新系统表。 可以通过系统视图查看系统表中的信息。 有关详细信息，请参阅[系统变量 (Transact-SQL)](../Topic/System%20Views%20\(Transact-SQL\).md)。  
  
 宽表  
 宽表使用[稀疏列](../../relational-databases/tables/use-sparse-columns.md)，从而将表可以包含的总列数增大为 30,000 列。 稀疏列是对 Null 值采用优化的存储方式的普通列。 稀疏列减少了 Null 值的空间需求，但代价是检索非 Null 值的开销增加。 宽表已定义了一个 [列集](../../relational-databases/tables/use-column-sets.md)，列集是一种非类型化的 XML 表示形式，它将表的所有稀疏列合并为一种结构化的输出。 索引数和统计信息数也分别增大为 1,000 和 30,000。 宽表行的最大大小为 8,019 个字节。 因此，任何特定行中的大部分数据都应为 NULL。 宽表中非稀疏列和计算列的列数之和仍不得超过 1,024。  
  
 宽表具有下列性能影响。  
  
-   宽表会增加维护表的索引的开销。 我们建议将宽表的索引数限制为业务逻辑所需的索引数。 索引数增加，DML 编译时和内存需求也会增加。 非聚集索引应当为应用到数据子集的筛选索引。 有关详细信息，请参阅 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。  
  
-   应用程序可以在宽表中动态添加和删除列。 当添加或删除列时，已编译的查询计划也将作废。 我们建议您设计与预定工作负荷相匹配的应用程序，以便使架构更改降至最少。  
  
-   当在宽表中添加和删除数据时，性能会受到影响。 必须针对预定工作负荷设计应用程序，以便使对表数据所做的更改降至最少。  
  
-   限制对宽表执行用于更新聚集键的多个行的 DML 语句。 编译和执行这些语句会需要非常多的内存资源。  
  
-   对宽表执行切换分区操作可能会很慢，并可能需要大量的内存才能加以处理。 性能和内存需求与源分区和目标分区中的列数成比例。  
  
-   用于更新宽表中特定列的更新游标应在 FOR UPDATE 子句中显式列出这些列。 这将有助于优化使用游标时的性能。  
  
## 公用表任务  
 下表提供指向与创建或修改表相关的常见任务的链接。  
  
|表任务|主题|  
|-----------------|-----------|  
|介绍如何创建表。|[创建表（数据库引擎）](../../relational-databases/tables/create-tables-database-engine.md)|  
|介绍如何删除表。|[删除表（数据库引擎）](../../relational-databases/tables/delete-tables-database-engine.md)|  
|介绍如何创建包含现有表中的一些列或所有列的表。|[复制表](../../relational-databases/tables/duplicate-tables.md)|  
|介绍如何重命名表。|[重命名表（数据库引擎）](../../relational-databases/tables/rename-tables-database-engine.md)|  
|介绍如何查看表的属性。|[查看表定义](../../relational-databases/tables/view-the-table-definition.md)|  
|介绍如何确定诸如视图或存储过程等其他对象是否取决于表。|[查看表的依赖关系](../../relational-databases/tables/view-the-dependencies-of-a-table.md)|  
  
 下表提供指向与创建或修改表中的列相关的常见任务的链接。  
  
|列任务|主题|  
|------------------|-----------|  
|介绍如何向现有表中添加列。|[向表中添加列（数据库引擎）](../../relational-databases/tables/add-columns-to-a-table-database-engine.md)|  
|介绍如何从表中删除列。|[从表中删除列](../../relational-databases/tables/delete-columns-from-a-table.md)|  
|介绍如何更改列的名称。|[重命名列（数据库引擎）](../../relational-databases/tables/rename-columns-database-engine.md)|  
|介绍如何通过仅复制列定义或者复制定义和数据将列从一个表复制到另一个表。|[将列从一个表复制到另一个表（数据库引擎）](../../relational-databases/tables/copy-columns-from-one-table-to-another-database-engine.md)|  
|介绍如何通过更改数据类型或其他属性来修改列定义。|[修改列（数据库引擎）](../../relational-databases/tables/modify-columns-database-engine.md)|  
|介绍如何更改列的显示顺序。|[更改表中的列顺序](../../relational-databases/tables/change-column-order-in-a-table.md)|  
|介绍如何在表中创建计算列。|[指定表中的计算列](../../relational-databases/tables/specify-computed-columns-in-a-table.md)|  
|介绍如何指定列的默认值。 如果未提供其他值，则使用此值。|[指定列的默认值](../../relational-databases/tables/specify-default-values-for-columns.md)|  
  
## 另请参阅  
 [主键和外键约束](../../relational-databases/tables/primary-and-foreign-key-constraints.md)   
 [唯一约束和 CHECK 约束](../../relational-databases/tables/unique-constraints-and-check-constraints.md)  
  
  