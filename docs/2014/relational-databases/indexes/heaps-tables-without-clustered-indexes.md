---
title: 堆（没有聚集索引的表）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- heaps
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: de71808c54264639aea82fe66cf23a7bfd6bd0ab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48098677"
---
# <a name="heaps-tables-without-clustered-indexes"></a>堆（没有聚集索引的表）
  堆是不含聚集索引的表。 可在存储为堆的表上创建一个或多个非聚集索引。 数据存储于堆中并且无需指定顺序。 通常，数据最初以行插入表时的顺序存储，但 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 可能会在堆中四处移动数据，以便高效地存储行；因此，无法预测数据顺序。 若要确保从堆返回的行的顺序，必须使用`ORDER BY`子句。 若要指定用于存储行的顺序，请对表创建聚集索引，以便表不是堆。  
  
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
  
## <a name="related-content"></a>相关内容  
 [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql)  
  
 [DROP INDEX (Transact-SQL)](/sql/t-sql/statements/drop-index-transact-sql)  
  
 [描述的聚集索引和非聚集索引](clustered-and-nonclustered-indexes-described.md)  
  
  
