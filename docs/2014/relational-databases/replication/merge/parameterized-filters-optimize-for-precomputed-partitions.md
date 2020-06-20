---
title: 使用预计算分区优化参数化筛选器性能 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- precomputed partitions [SQL Server replication]
- merge replication precomputed partitions [SQL Server replication]
- merge replication precomputed partitions [SQL Server replication], about precomputed partitions
ms.assetid: 85654bf4-e25f-4f04-8e34-bbbd738d60fa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4ad0a33f0a5951256ff94bc78e7f09a88c05f227
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010422"
---
# <a name="optimize-parameterized-filter-performance-with-precomputed-partitions"></a>使用预计算分区优化参数化筛选器的性能
  预计算分区是一种性能优化方法，可用于已筛选的合并发布。 预计算分区也是在已筛选的发布上使用逻辑记录的一项要求。 有关逻辑记录的详细信息，请参阅[通过逻辑记录对相关行的更改进行分组](group-changes-to-related-rows-with-logical-records.md)。  
  
 订阅服务器与发布服务器同步时，发布服务器必须计算订阅服务器的筛选器，以确定哪些行属于该订阅服务器的分区或数据集。 我们将为接收已筛选数据集的每个订阅服务器确定发布服务器上的更改的分区成员身份这一过程称为“分区计算” **。 如果没有预计算分区，那么，自上次为特定订阅服务器运行合并代理之后，对发布服务器上已筛选列每进行一次更改都必须执行分区计算，而且对与该发布服务器同步的每个订阅服务器都要重复这一过程。  
  
 但是，如果发布服务器和订阅服务器在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本上运行，并且您使用的是预计算分区，则在发布服务器上进行的所有更改的分区成员身份在进行更改时将预计算并持久保存。 因此，当订阅服务器与发布服务器同步时，它可以立即开始下载与其分区相关的更改，而不必执行分区计算过程。 当发布中有大量更改、订阅服务器或项目时，这样可以显著提高性能。  
  
 除了使用预计算分区外，预先生成快照和/或允许订阅服务器在第一次同步时还请求生成快照和应用快照。 使用以上选项中的一个或两个可以为使用参数化筛选器的发布提供快照。 如果未指定任一选项，将使用一系列的 SELECT 和 INSERT 语句初始化订阅，而不是使用 **bcp** 实用工具；此过程的速度将更慢。 有关详细信息，请参阅 [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
 **使用预计算分区**  
  
 默认情况下，在遵循上述指导原则的所有新发布和现有发布上均启用了预计算分区。 可通过 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或通过编程方式更改此设置。 有关详细信息，请参阅 [Optimize Parameterized Row Filters](../publish/optimize-parameterized-row-filters.md)。  
  
## <a name="requirements-for-using-precomputed-partitions"></a>使用预计算分区的要求  
 如果满足下列要求，默认情况下创建新的合并复制时将启用预计算分区，而现有的发布将自动升级以使用此功能。 如果发布不满足下列要求，可对其先进行更改，然后即可启用预计算分区。 如果有些项目满足这些要求而有些不满足，请考虑创建两个发布，为其中一个发布启用预计算分区。  
  
### <a name="requirements-for-filter-clauses"></a>筛选器子句的要求  
  
-   参数化行筛选器中使用的任何函数（如 HOST_NAME() 和 SUSER_SNAME()），都应直接出现在参数化筛选器子句中，而不能嵌套在视图或动态函数内。 有关这些函数的详细信息，请参阅 [HOST_NAME (Transact-SQL)](/sql/t-sql/functions/host-name-transact-sql)、[SUSER_SNAME (Transact-SQL)](/sql/t-sql/functions/suser-sname-transact-sql) 和[参数化行筛选器](parameterized-filters-parameterized-row-filters.md)。  
  
-   创建分区后，不应更改为每个订阅服务器返回的值。 例如，如果在筛选器中使用 HOST_NAME()（且不覆盖 HOST_NAME() 值），请不要更改订阅服务器上的计算机名称。  
  
-   联接筛选器不应包含动态函数（如 HOST_NAME() 和 SUSER_SNAME()，此类函数会根据正在同步的订阅服务器计算出不同的值）。 只有参数化行筛选器可以包含动态函数。  
  
-   筛选器子句中不能使用不确定性函数。 有关不确定性函数的详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
-   在联接筛选器子句或参数化筛选器子句中引用的视图不应包含动态函数。  
  
-   发布中不应有循环联接筛选器关系。  
  
### <a name="database-collation"></a>数据库排序规则  
  
-   如果使用了预计算分区，进行比较时始终使用数据库的排序规则，而不使用表或列的排序规则。 请参考以下方案：  
  
    -   具有区分大小写排序规则的数据库包含一个具有不区分大小写排序规则的表。  
  
    -   该表包含一个 **ComputerName**列，它与参数化筛选器中的订阅服务器的主机名相比较。  
  
    -   该表在此列中包含一个值为“MYCOMPUTER”的行和一个值为“mycomputer”的行。  
  
     如果订阅服务器与主机名“mycomputer”同步，则订阅服务器只能收到一行，因为比较是区分大小写的（数据库的排序规则）。 如果未使用预计算分区，订阅服务器会收到这两行，因为该表具有不区分大小写的排序规则。  
  
## <a name="performance-of-precomputed-partitions"></a>预计算分区的性能  
 在将更改从订阅服务器上载到发布服务器时，尽管使用预计算分区会产生少量的性能开销，但大部分合并处理时间用于计算分区以及将更改从发布服务器下载到订阅服务器上，所以净的性能收益仍然很显著。 根据并发同步的订阅服务器的数目以及将行从一个分区移动到另一分区的每个同步的更新数目的不同，性能收益也会有所不同。  
  
## <a name="see-also"></a>另请参阅  
 [参数化行筛选器](parameterized-filters-parameterized-row-filters.md)  
  
  
