---
title: 使用临时数据库
description: SQL Server 并行数据仓库（PDW）在加载过程中使用临时数据库临时存储数据。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: dcd7f95833695cc5f9f791d83a6221c35e88f58e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400283"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>在并行数据仓库（PDW）中使用临时数据库
SQL Server 并行数据仓库（PDW）在加载过程中使用临时数据库临时存储数据。 默认情况下，SQL Server PDW 使用目标数据库作为临时数据库，这可能会导致表碎片。 若要减少表碎片，可以创建用户定义的临时数据库。 或者，如果不考虑从负载故障中回滚，则可以使用 fastappend 加载模式来提高性能，方法是跳过临时表并直接加载到目标表中。  
  
## <a name="StagingDatabase"></a>临时数据库基础知识  
*临时数据库*是用户创建的 PDW 数据库，用于在将数据加载到设备时暂时存储数据。 如果为负载指定了临时数据库，则设备首先将数据复制到临时数据库，然后将临时数据库中的临时表中的数据复制到目标数据库中的永久表中。  
  
如果没有为负载指定暂存数据库，SQL ServerPDW 将在目标数据库中创建临时表，并使用这些表存储加载的数据，然后将加载的数据插入到永久目标表中。  
  
当负载使用*fastappend 模式*时，SQL ServerPDW 将跳过使用临时表，并将数据直接追加到目标表。 对于从应用程序的角度而言，将数据加载到作为临时表的表中的 ELT 方案，fastappend 模式将提高其负载性能。 例如，ELT 进程可以将数据加载到临时表中，通过清除和 duping 来处理数据，然后将数据插入到目标事实数据表中。 在这种情况下，PDW 在将数据插入到应用程序的临时表之前，不需要先将数据加载到内部临时表中。 Fastappend 模式避免了额外的负载步骤，从而显著提高了负载性能。 若要使用 fastappend 模式，你必须使用多事务模式，这意味着从失败或中止的负载中进行的恢复必须由你自己的加载进程处理。  
  
**临时数据库的优点**  
  
临时数据库的主要优点是减少表碎片。 如果未使用临时数据库，则会将数据加载到目标数据库中的临时表中。 在目标数据库中创建和删除临时表时，临时表和永久表的页将变得交错。 随着时间的推移，会发生表碎片并降低性能。 与此相反，临时数据库可确保在独立于永久表的文件空间中创建和删除临时表。  
  
**临时数据库表结构**  
  
每个数据库表的存储结构取决于目标表。  
  
-   对于加载到堆或聚集列存储索引中，临时表为堆集。  
  
-   对于加载到行存储聚集索引中的临时表，临时表是一个行存储聚集索引。  
  
## <a name="Permissions"></a>权限  
需要对临时数据库具有 CREATE 权限（用于创建临时表）。 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="CreatingStagingDatabase"></a>创建临时数据库的最佳做法  
  
1.  每个设备只能有一个临时数据库。 所有目标数据库的所有加载作业都可以共享临时数据库。  
  
2.  临时数据库的大小是特定于客户的。 最初，在首次填充设备时，临时数据库应足够大以容纳初始加载作业。 由于多个加载可能会并发发生，因此这些加载作业很大。 初始加载作业完成并且系统投入生产后，每个加载作业的大小可能较小。 当负载较小时，可以减小暂存数据库的大小，以适应较小的负载大小。 若要减小其大小，可以删除临时数据库，并使用较小的分配重新创建它，或者可以使用[ALTER database](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)语句。  
  
    创建临时数据库时，请使用以下准则。  
  
    -   复制的表大小应为将同时加载的所有复制表的估计大小（每个计算节点）。 大小通常为 25-30 GB。  
  
    -   分布式表的大小应为将同时加载的所有分布式表的估计大小（每个设备）。  
  
    -   日志大小通常类似于复制的表大小。  
  
## <a name="Examples"></a>示例  
  
### <a name="a-create-a-staging-database"></a>A. 创建临时数据库 
以下示例创建一个临时数据库 Stagedb，用于设备上的所有负载。 假设你估计每5个复制表的大小为 5 GB，每个表都将同时加载。 此并发会导致为复制的大小分配至少 25 GB。 假设你预计有六个大小为100、200、400、500、500和 550 GB 的分布式表将同时加载。 这种并发会导致为分布式表大小分配至少 2250 GB。  
  
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
  
