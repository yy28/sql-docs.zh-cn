---
title: "为并行数据仓库中创建的临时数据库"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "SQL Server 并行数据仓库 (PDW) 使用临时数据库的加载过程中临时存储数据。"
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 6d0b2726-4772-4858-b700-885cc12219b2
caps.latest.revision: "20"
ms.openlocfilehash: 073dbb385d34d67b9274ac46828df5887abfe5a4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="staging-database"></a>临时数据库 
SQL Server 并行数据仓库 (PDW) 使用临时数据库的加载过程中临时存储数据。 默认情况下，SQL Server PDW 作为临时数据库，这可能导致表碎片使用目标数据库。 若要减少表碎片，可以创建用户定义的临时数据库。 或者，从加载失败的回滚并不是问题，你可以使用 fastappend 加载模式通过跳过临时表并加载直接到目标表来提高性能。  
  
## <a name="StagingDatabase"></a>暂存数据库基础知识  
A*暂存数据库*是用户创建 PDW 数据库加载到设备时暂时存储数据。 指定一个临时数据库时的负载，设备会首先将数据复制到临时数据库，然后将数据从临时数据库中的临时表复制到目标数据库中永久表。  
  
如果临时数据库未指定的负载，SQL ServerPDW 目标数据库中创建临时表并使用它们来存储加载的数据之前它将加载的数据插入到永久目标表。  
  
当负载使用*fastappend 模式*，SQL ServerPDW 跳过完全使用临时表，并将数据追加直接到目标表。 Fastappend 模式可以提高到是从应用程序角度来看一个临时表的表数据的加载位置的 ELT 方案的负载性能。 例如，一个 ELT 过程无法将数据加载到临时表、 清理和消除重复，处理数据和再将数据插入到目标事实表。 在这种情况下，不需 PDW 的第一次加载到内部临时表中的数据在应用程序的临时表中插入数据之前。 Fastappend 模式可避免额外负载步骤中，这可以显著加快加载性能。 请注意，若要使用的 fastappend 模式，你必须使用多事务模式下，这意味着从失败或已中止负载恢复必须由你自己的加载过程。  
  
**暂存数据库的好处**  
  
临时数据库的主要好处是减少表碎片。 如果未使用临时数据库，则会将数据加载到目标数据库中的临时表。 如果临时表获取创建和删除目标数据库中，临时表和永久表的页变为交错。 随着时间推移，这将导致表碎片，并会降低性能。 与此相反，创建并在单独的文件空间与永久表中删除临时表，可确保临时数据库。  
  
**暂存数据库表结构**  
  
每个数据库表的存储结构取决于目标表。  
  
-   对于加载到堆或聚集列存储索引，临时表是堆。  
  
-   对于加载到行存储聚集索引，临时表是行存储聚集的索引。  
  
## <a name="Permissions"></a>Permissions  
将在临时数据库要求 （用于创建临时表） 的创建权限。 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="CreatingStagingDatabase"></a>创建一个临时数据库的最佳做法  
  
1.  只应为每个设备的一个临时数据库。 这可由所有目标数据库的所有加载作业共享。  
  
2.  临时数据库的大小是特定于客户的。 最初，首先填充装置时, 临时数据库应足够大以容纳的初始加载作业。 这些加载作业往往很大，因为多个负载可能会同时发生。 初始加载作业已完成，并且系统处于生产环境后，每个负载作业的大小很可能较小。 如果发生这种情况，则可以可以减少临时数据库，以适应较小的负载大小的大小。 若要减少的大小，可以删除临时数据库和数据透视表重新创建较小的大小分配，或者你可以使用[ALTER DATABASE](../t-sql/statements/alter-database-parallel-data-warehouse.md)语句。  
  
    创建临时数据库时，使用以下准则。  
  
    -   复制的表大小应为每个计算节点，将同时加载的所有复制表的估计的大小。 这通常是 25-30 GB。  
  
    -   分布式的表大小应为每个设备，将同时加载的所有分布式表的估计的大小。  
  
    -   日志大小为通常类似于复制的表大小。  
  
## <a name="Examples"></a>示例  
  
### <a name="a-create-a-staging-database"></a>A. 创建一个临时数据库 
下面的示例创建一个临时数据库，Stagedb，用于在设备上的所有负载。 假设你估计五个复制表的大小将同时加载 5 GB。 这会导致复制大小分配至少 25 GB。 假设你估计六个分布式表的大小 100，200、 400、 500、 500 和 550 GB 将同时加载。 这会导致为分布式的表大小分配至少 2250 GB。  
  
```sql  
CREATE DATABASE Stagedb  
WITH (  
  
    AUTOGROW = ON,  
  
    REPLICATED_SIZE = 25 GB,  
  
    DISTRIBUTED_SIZE = 2250 GB,  
  
    LOG_SIZE = 25 GB  
  
);  
```  

<!-- MISSING LINKS
 
## See Also  
[Common metadata query examples](metadata-query-examples.md)  

-->
  
