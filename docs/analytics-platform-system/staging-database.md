---
title: 使用临时数据库的并行数据仓库 |Microsoft Docs
description: SQL Server 并行数据仓库 (PDW) 使用临时数据库来暂时在加载过程中存储数据。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 52ede16185515c3df00ff21ece784d62eec984ef
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52396512"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>使用并行数据仓库 (PDW) 的临时数据库
SQL Server 并行数据仓库 (PDW) 使用临时数据库来暂时在加载过程中存储数据。 默认情况下，SQL Server PDW 作为临时数据库，可能会导致表碎片使用目标数据库。 若要减少表的碎片，可以创建用户定义的临时数据库。 或者，当从加载失败的回滚不是一个问题，可以使用 fastappend 加载模式下通过跳过的临时表并加载直接到目标表来提高性能。  
  
## <a name="StagingDatabase"></a>暂存数据库基础知识  
一个*暂存数据库*是用户创建用于加载到设备时暂时存储数据的 PDW 数据库。 当在负载指定一个临时数据库时，设备将首先将数据复制到临时数据库，然后将数据从临时数据库中的临时表复制到目标数据库中的永久表。  
  
如果没有为负载指定一个临时数据库，SQL ServerPDW 将在目标数据库中创建临时表，并使用它们来存储加载的数据之前它将加载的数据插入到永久目标表。  
  
当使用负载*fastappend 模式*，SQL ServerPDW 将跳过完全使用临时表，并将数据追加直接到目标表。 Fastappend 模式可以提高负载性能 ELT 方案到是从应用程序角度来看一个临时表的表加载数据的位置。 例如，ELT 过程无法将数据加载到临时表、 清理和取消其执行重复，处理的数据，然后将数据插入到目标事实数据表。 在这种情况下，它不需要为 PDW 第一次加载到内部临时表中的数据之前将数据插入到应用程序的临时表。 Fastappend 模式可避免额外的负载步骤中，这将显著提高负载性能。 若要使用 fastappend 模式，必须使用多事务模式下，这意味着，必须由您自己的加载进程处理失败或已中止负载进行恢复。  
  
**临时数据库的好处**  
  
临时数据库的主要好处是减少表的碎片。 如果未使用临时数据库，则会将数据加载到目标数据库中的临时表。 当临时表获取创建和删除目标数据库中时，临时表和永久表的页成为交错。 随着时间的推移表碎片会发生，并会降低性能。 与此相反，临时数据库可确保临时表创建和删除单独的文件空间比永久表中。  
  
**临时数据库表结构**  
  
每个数据库表的存储结构取决于目标表。  
  
-   对于加载到堆或聚集列存储索引，临时表是堆。  
  
-   对于到行存储聚集索引中的负载，临时表是行存储聚集的索引。  
  
## <a name="Permissions"></a>Permissions  
将在临时数据库要求 （用于创建临时表） 创建权限。 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="CreatingStagingDatabase"></a>创建一个临时数据库的最佳做法  
  
1.  应仅有一个临时数据库，每个设备。 临时数据库可由所有目标数据库的所有加载作业共享。  
  
2.  临时数据库的大小是特定于客户的。 最初，当首次填充设备时，临时数据库应足够大以容纳的初始加载作业。 这些加载作业往往很大，因为可以同时发生多个加载。 初始加载作业已完成，并且系统是在生产环境中的每个负载作业大小后，可能是较小。 加载较小，可以减少要适应较小的负载大小的临时数据库的大小。 若要减少的大小，可以删除临时数据库，然后重新创建具有较小的大小分配，也可以使用[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)语句。  
  
    创建临时数据库时，使用以下指导原则。  
  
    -   复制的表大小应为每个计算节点，将同时加载的所有复制表的估计的大小。 大小通常是 25 到 30 GB。  
  
    -   分布式的表大小应为每个设备，将同时加载的所有分布式表的估计的大小。  
  
    -   日志大小为通常类似于复制的表大小。  
  
## <a name="Examples"></a>示例  
  
### <a name="a-create-a-staging-database"></a>A. 创建一个临时数据库 
下面的示例创建一个临时数据库，Stagedb，用于在设备上的所有负载。 假设您估计五个复制将同时加载 5 GB 大小的表。 这种并发会导致复制大小分配至少 25 GB。 假设您估算六个分布式表的大小 100，200、 400、 500、 500 和 550 GB 将同时加载。 这种并发会导致为分布式的表的大小分配至少 2250 GB。  
  
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
  
