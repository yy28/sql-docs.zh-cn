---
title: "堆（没有聚集索引的表）| Microsoft Docs"
ms.custom: 
ms.date: 11/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- heaps
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cae45be3e215c24dd437502f81a870f14d453f3d
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="heaps-tables-without-clustered-indexes"></a>堆（没有聚集索引的表）
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  堆是不含聚集索引的表。 可在存储为堆的表上创建一个或多个非聚集索引。 数据存储于堆中并且无需指定顺序。 通常，数据最初以行插入表时的顺序存储，但 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 可能会在堆中四处移动数据，以便高效地存储行；因此，无法预测数据顺序。 若要确保从堆返回的行的顺序，您必须使用 **ORDER BY** 子句。 若要指定用于存储行的顺序，请对表创建聚集索引，以便表不是堆。  
  
> [!NOTE]  
>  有时候可能有必要将表保留为堆，而不是创建聚集索引，但高效率地使用堆需要较高的技能。 大多数表应该具有仔细选择的聚集索引，除非有足够的理由将表保留为堆。  
  
## <a name="when-to-use-a-heap"></a>何时使用堆  
 如果某个表是堆并且不具有任何非聚集索引，则必须检查整个表（表扫描）以便找到任何行。 这在表很小（例如公司 12 个地区办事处的列表）时是可接受的。  
  
 在将某个表存储为堆时，通过引用由文件号、数据页码和页上的槽构成的行标识符 (RID)，标识单独行。 行 ID 是一个小且高效的结构。 有时候，在数据始终通过非聚集索引访问并且 RID 小于聚集索引键时，数据结构设计师会使用堆。  
  
## <a name="when-not-to-use-a-heap"></a>何时不使用堆  
 在经常以排序后的顺序返回数据时，不要使用堆。 排序列上的聚集索引可以避免排序操作。  
  
 在数据经常组合在一起时，不要使用堆。 数据必须首先进行排序，然后才能分组，并且排序列上的聚集索引可以避免排序操作。  
  
 在经常从表查询数据范围时，不要使用堆。  范围列上的聚集索引将避免对整个堆进行排序。  
  
 在不存在非聚集索引并且表比较大时，不要使用堆。 在某一堆中，若要找到任何行，必须读取该堆的所有行。  
  
## <a name="managing-heaps"></a>管理堆  
 若要创建堆，请创建没有聚集索引的表。 如果表已具有某一聚集索引，则删除该聚集索引以便将该表返回到某一堆。  
  
 若要删除堆，请在该堆上创建聚集索引。  
  
 若要重新生成堆以便回收浪费的空间，请在该堆上创建一个聚集索引，然后删除该聚集索引。  
  
> [!WARNING]  
>  创建或删除聚集索引要求重写整个表。 如果该表具有非聚集索引，则只要更改聚集索引，就必须全都重新创建所有非聚集索引。 因此，从堆更改为聚集索引结构或反之可能占用大量时间，并且要求足够的磁盘空间以便对 tempdb 中的数据重新进行排序。  

## <a name="heap-structures"></a>堆结构


堆是不含聚集索引的表。 堆的 [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)中具有一行，对于堆使用的每个分区，都有 `index_id = 0` 。 默认情况下，一个堆有一个分区。 当堆有多个分区时，每个分区有一个堆结构，其中包含该特定分区的数据。 例如，如果一个堆有四个分区，则有四个堆结构；每个分区有一个堆结构。

根据堆中的数据类型，每个堆结构将有一个或多个分配单元来存储和管理特定分区的数据。 每个堆中每个分区至少有一个 `IN_ROW_DATA` 分配单元。 如果堆包含大型对象 (LOB) 列，则该堆的每个分区还将有一个 `LOB_DATA` 分配单元。 如果堆包含超过 8,060 字节的行大小限制的变量长度列，则它的每个分区中还会有一个 `ROW_OVERFLOW_DATA` 分配单元。

`first_iam_page` 系统视图中的列 `sys.system_internals_allocation_units` 指向 IAM 页链中的第一个 IAM 页，该 IAM 页链可管理分配给特定分区中的堆的空间。 SQL Server 使用 IAM 页在堆之间移动。 堆内的数据页和行没有任何特定的顺序，也不链接在一起。 数据页之间唯一的逻辑连接是记录在 IAM 页内的信息。

> [!IMPORTANT]  
> `sys.system_internals_allocation_units` 系统视图保留为仅供 Microsoft SQL Server 内部使用。 不保证以后的兼容性。
 
可以通过扫描 IAM 页对堆进行表扫描或串行读操作来找到容纳该堆的页的扩展盘区。 因为 IAM 按扩展盘区在数据文件内存在的顺序表示它们，所以这意味着串行堆扫描连续沿每个文件进行。 使用 IAM 页设置扫描顺序还意味着堆中的行一般不按照插入的顺序返回。

下图说明了 SQL Server 数据库引擎如何使用 IAM 页检索单个分区堆中的数据行。 

![iam_heap](../../relational-databases/indexes/media/iam-heap.gif)

  
## <a name="related-content"></a>相关内容  
 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)  
  
 [DROP INDEX (Transact-SQL)](../../t-sql/statements/drop-index-transact-sql.md)  
  
 [描述的聚集索引和非聚集索引](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)  
  
  

