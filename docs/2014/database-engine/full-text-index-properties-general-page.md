---
title: 全文索引属性（"常规" 页） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.general.f1
ms.assetid: f4dff61c-8c2f-4ff9-abe4-70a34421448f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: a240ed4e3788d65ab795d8680dc93f253cfde059
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62778938"
---
# <a name="full-text-index-properties-general-page"></a>全文索引属性（“常规”页）
  **查看或更改全文索引的可修改属性**  
  
-   [管理全文索引](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>UIElement 列表  
 **全文目录**  
 显示全文索引所关联的全文目录的名称。  
  
 **Database**  
 显示驻留全文索引的数据库的名称。  
  
 **表**  
 显示定义全文索引的表的名称。  
  
 **全文索引键**  
 显示全文索引关键的名称，此键是表的单个列上的唯一索引。  
  
 **表全文填充状态**  
 显示全文索引表的填充状态。  
  
 可能的值如下：  
  
 0 = 空闲。  
  
 1 = 完整填充正在进行中。  
  
 2 = 增量填充正在进行中。  
  
 3 = 跟踪更改的传播正在进行中。  
  
 4 = 后台更新索引正在进行中，比如自动更改跟踪。  
  
 5 = 全文索引已中止或暂停。  
  
 **活动全文索引**  
 指示表是否有活动的全文索引。  
  
 1 = True  
  
 0 = False  
  
 **全文索引文件组**  
 全文索引所属的文件组。  
  
 **全文索引非索引字表**  
 当前与全文索引关联的非索引字表。 非索引字表是 [非索引字](../relational-databases/search/full-text-search.md)的列表。 与全文索引关联的非索引字表（如果有）适用于该索引的全文查询。 您可以通过从列表中选择** \<"关闭>** ，从索引中删除非索引字表，也可以选择其他非索引字表;系统>指示系统非索引字表。 ** \<**  
  
 **创建非索引字表**  
  
-   [为全文搜索配置和管理非索引字和非索引字表](../relational-databases/search/full-text-search.md)  
  
 **搜索属性列表**  
 当前与全文索引关联的搜索属性列表（如果有）。 搜索属性列表指定一组文档属性，在填充关联的全文索引时这些文档属性包括在其中。 有关详细信息，请参阅 [使用搜索属性列表搜索文档属性](../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
 Off>表示当前没有与索引关联的搜索属性列表。 ** \<** 您可以通过从列表中选择** \<"关闭>** ，从索引中删除当前搜索属性列表，也可以从列表中选择不同的搜索属性列表。 在此处只列出当前数据库中的搜索属性列表。  
  
> [!NOTE]  
>  您可以将给定的搜索属性列表与同一数据库中的多个全文索引相关联。  
  
 **创建搜索属性列表**  
  
-   [使用搜索属性列表搜索文档属性](../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
 **表全文项计数**  
 指示成功执行了全文索引的行数。  
  
 此属性对应于由 OBJECTPROPERTYEX [!INCLUDE[tsql](../includes/tsql-md.md)] 函数返回的 `TableFulltextItemCount` 属性。  
  
 **已处理的表全文文档数**  
 显示自从全文索引开始以来已处理的行数。 在为进行全文搜索而正在编制索引的表中，将一个行的所有列视为要编制索引的文档的一部分。 已删除的行不被计数。  
  
|||  
|-|-|  
|0|指示全文索引已完成，并且没有活动填充。|  
|> 0|对于活动填充，指示自从执行任何以下操作以来由插入或更新操作所处理的文档数：填充、启用具有后台更新索引填充功能的更改跟踪（比如自动更改跟踪）、更改全文索引架构、重建全文目录、重新启动 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的实例等等。|  
  
 **表全文挂起更改**  
 要处理的挂起更改跟踪项的数目。  
  
 0 = 不启用更改跟踪。  
  
 NULL = 表没有全文索引。  
  
 **表全文失败计数**  
 全文搜索未索引的行数。  
  
 0 = 填充已完成。  
  
 \>0 = 以下项之一：  
  
-   自从完整、增量或手动的更改跟踪填充开始以来未索引的文档数。  
  
-   对于有后台更新索引的更改跟踪，则是自从填充开始以来未索引的行数，或重新启动填充。 这可以由架构更改、目录重建、服务器重新启动等等导致。  
  
 **全文索引已启用**  
 指定是否已启用全文索引。  
  
|||  
|-|-|  
|**True**|启用|  
|**False**|禁用|  
  
 **更改跟踪**  
 指定表是否启用了全文更改跟踪，如果启用，则是什么种类。 全文更改跟踪用于记录已设置全文索引的表或索引视图中已修改的行。 这些更改可以传播到全文索引。  
  
 **“更改跟踪”** 值如下：  
  
|||  
|-|-|  
|**非**|不以基础数据的更改来更新全文索引。|  
|**手动**|基础数据发生更改时，不自动更新全文索引。 但是，会维护基础数据的更改，并且可以使用 SQL Server 代理定期或手动将它们传播到 全文索引。|  
|**自动**|当基表中的基础数据发生更改时，则自动更新全文索引。|  
  
 **重新填充索引**  
 单击它可以在退出对话框后启动对全文索引的填充。 请选择以下填充类型之一：  
  
|||  
|-|-|  
|**达到**|在表的完整填充期间，为所有行生成索引条目。|  
|**增量**|增量填充在全文索引中更新上次填充的当时或之后添加、删除或修改的行。 执行增量填充需要基表包含一个 `timestamp` 数据类型的列。|  
|**Update**|一旦修改基表中的数据，将更新全文索引。|  
  
## <a name="see-also"></a>另请参阅  
 [全文搜索入门](../relational-databases/search/get-started-with-full-text-search.md)  
  
  
