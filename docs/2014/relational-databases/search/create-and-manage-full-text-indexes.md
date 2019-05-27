---
title: 创建和管理全文索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], about
ms.assetid: f8a98486-5438-44a8-b454-9e6ecbc74f83
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a41f11b200ffe5dfc91479ea54095fd24c90699a
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011549"
---
# <a name="create-and-manage-full-text-indexes"></a>创建和管理全文索引
  全文引擎使用全文索引中的信息来编译可快速搜索表中的特定词或词组的全文查询。 全文索引将有关重要的词及其位置的信息存储在数据库表的一列或多列中。 全文索引是一种特殊类型的基于标记的功能性索引，它是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]全文引擎生成和维护的。 生成全文索引的过程不同于生成其他类型的索引。 全文引擎并非基于特定行中存储的值来构造 B 树结构，而是基于要编制索引的文本中的各个标记来生成倒排、堆积且压缩的索引结构。  全文索引大小仅受运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机的可用内存资源限制。  
  
 从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]开始，全文索引与数据库引擎集成在一起，而不是像 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]早期版本那样位于文件系统中。 对于新数据库，全文目录现在为不属于任何文件组的虚拟对象；它仅是一个表示一组全文索引的逻辑概念。 然而，请注意，在升级 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库（即包含数据文件的任意全文目录）的过程中，将创建一个新文件组。有关详细信息，请参阅 [升级全文搜索](upgrade-full-text-search.md)。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中，全文引擎位于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中，而不是位于单独的服务中。 通过将全文引擎集成到数据库引擎中，可提高全文可管理性和总体性能，并进一步优化了混合查询。  
  
 每个表只允许有一个全文索引。 若要对某个表创建全文索引，该表必须具有一个唯一且非 Null 的列。 你可以对以下类型的列创建全文索引：`char`、`varchar`、`nchar`、`nvarchar`、`text`、`ntext`、`image`、`xml`、`varbinary` 和 `varbinary(max)`，从而可对这些列进行全文搜索。 对数据类型为 `varbinary`、`varbinary(max)`、`image` 或 `xml` 的列创建全文索引需要您指定类型列。 *类型列*是用来存储每行中文档的文件扩展名（.doc、.pdf、xls 等）的表列。  
  
 创建和维护全文索引的过程称为“填充”（也称为“爬网”）。 有三种类型的全文索引填充：完全填充、基于更改跟踪的填充和基于时间戳的增量式填充。 有关详细信息，请参阅 [填充全文索引](populate-full-text-indexes.md)。  
  
##  <a name="tasks"></a> 常见任务  
 **若要创建全文索引**  
  
-   [CREATE FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
 **若要更改全文索引**  
  
-   [ALTER FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
 **若要删除全文索引**  
  
-   [DROP FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/drop-fulltext-index-transact-sql)  
  
 [本主题内容](#top)  
  
##  <a name="structure"></a> 全文索引结构  
 对全文索引的结构的良好了解将帮助您了解全文引擎的工作方式。 本主题使用 **中的** Document [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 表的以下摘录部分作为示例表。 此摘录部分仅显示该表的两个列（ **DocumentID** 列和 **Title** 列）和三行。  
  
 对于本示例，我们假定已对“标题”列创建全文索引。  
  
|DocumentID|标题|  
|----------------|-----------|  
|1|Crank Arm and Tire Maintenance|  
|2|Front Reflector Bracket and Reflector Assembly 3|  
|3|Front Reflector Bracket Installation|  
  
 例如，下表（显示 Fragment 1）描述对“Document”表的“Title”列创建的全文索引的内容。 与该表呈现的信息相比，全文索引包含更多信息。 该表是全文索引的逻辑表示形式，并且仅为演示目的提供。 行以压缩格式存储，以优化磁盘的使用。  
  
 注意，数据已从原始文档倒排。 发生数据倒排是因为关键字映射到文档 ID。 因此，全文索引通常称为倒排索引。  
  
 还要注意，已从全文索引中删除关键字“and”。 这样做是因为“and”是非索引字，从全文索引中删除非索引字可以大幅节省磁盘空间，并因此提高查询性能。 有关非索引字的详细信息，请参阅 [为全文搜索配置和管理非索引字和非索引字表](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
 **碎片 1**  
  
|关键字|ColId|DocId|出现次数|  
|-------------|-----------|-----------|----------------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|维护|1|1|5|  
|Front|1|2|1|  
|Front|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|Bracket|1|3|3|  
|Assembly|1|2|6|  
|3|1|2|7|  
|安装|1|3|4|  
  
 **Keyword** 列包含在创建索引时提取的单个标记的表示形式。 断字符可确定组成标记的词。  
  
 “ColId” 列包含的值对应于已建立全文索引的特定列。  
  
 `DocId`列包含八字节整数映射到全文索引表中的特定全文键值的值。 如果全文键不是整数数据类型，则需要此映射。 在这种情况下，全文索引之间的映射键值和`DocId`值保留在单独的表名为 DocId Mapping 表。 若要查询这些映射，请使用 [sp_fulltext_keymappings](/sql/relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql) 系统存储过程。 若要满足搜索条件，则上述表中的 DocId 值需要与 DocId Mapping 表联接，以便从所查询的基表中检索行。 如果基表的全文键值是整数类型，则该值直接充当 DocId，而不需要映射。 因此，使用整数全文键值有助于优化全文查询。  
  
 **Occurrence** 列包含整数值。 对于每个 DocId 值，均有一个 Occurrence 值的列表对应于该 DocId 值中特定关键字的相对字偏移量。 位置值用于确定短语或邻近匹配项，例如具有相邻位置值的短语。 它们还用于计算相关性分数，例如记分时可能会用某个关键字在 DocId 中的出现次数。  
  
 [本主题内容](#top)  
  
##  <a name="fragments"></a> 全文索引碎片  
 逻辑全文索引通常拆分到多个内部表中。 每个内部表称为一个全文索引碎片。 这些碎片中的某一些可能包含比其他碎片更新的数据。 例如，如果用户更新其 DocId 是 3 的以下行，并且该表可自动跟踪更改，则会创建新的碎片。  
  
|DocumentID|标题|  
|----------------|-----------|  
|3|Rear Reflector|  
  
 在下面的示例（显示 Fragment 2）中，碎片中包含比 Fragment 1 中更新的关于 DocId 3 的数据。 因此，当用户查询“Rear Reflector”时，会将 Fragment 2 中的数据用于 DocId 3。 每个碎片都用一个创建时间戳来标记，可以使用 [sys.fulltext_index_fragments](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql) 目录视图查询该时间戳。  
  
 **碎片 2**  
  
|关键字|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Rear|1|3|1|  
|Reflector|1|3|2|  
  
 从 Fragment 2 可以看到，全文查询需要在内部查询每个碎片，并放弃更旧的条目。 因此，全文索引中太多的全文索引碎片会导致查询性能大幅下降。 若要减少碎片数，请使用 [ALTER FULLTEXT CATALOG](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的 REORGANIZE 选项来重新组织全文目录。 此语句将执行一次 *主合并*，主合并将碎片合并成一个更大的碎片，并从全文索引中删除所有过时的条目。  
  
 经过重新组织后，示例索引会包含以下行：  
  
|关键字|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|维护|1|1|5|  
|Front|1|2|1|  
|Rear|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|Assembly|1|2|6|  
|3|1|2|7|  
  
 [本主题内容](#top)  
  
  
