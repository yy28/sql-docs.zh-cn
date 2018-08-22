---
title: 与内存优化哈希索引的常见性能问题故障排除 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1954a997-7585-4713-81fd-76d429b8d095
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 28fea2aed82e86d58264311914a341fb6ecca4fc
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395832"
---
# <a name="troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes"></a>对内存优化哈希索引的常见性能问题进行故障排除
  本主题主要针对解决与哈希索引有关的常见问题。  
  
## <a name="search-requires-a-subset-of-hash-index-key-columns"></a>搜索要求哈希索引键列的子集  
 **问题：** 哈希索引需要的所有值以计算哈希值，索引键列和哈希表中定位相应行。 因此，如果某个查询在 WHERE 子句中仅包含针对索引键的某个子集的相等谓词，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将无法使用索引查找在 WHERE 子句中定位与这些谓词相对应的行。  
  
 相反，有序索引（例如基于磁盘的非聚集索引和内存优化的非聚集索引）支持在索引键列的子集上的索引查找，只要它们是索引中的首列。  
  
 **症状：** 这会导致性能下降，作为[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]需要执行全表扫描而不是索引查找，这通常是更快的操作。  
  
 **如何进行故障排除：** 除了性能下降，检查查询计划将显示扫描，而不是索引查找。 如果查询相对简单，则对查询文本和索引定义的检查还将显示搜索是否要求索引键列的子集。  
  
 请参考下面的表和查询：  
  
```tsql  
CREATE TABLE [dbo].[od]  
(  
     o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
     CONSTRAINT PK_od PRIMARY KEY NONCLUSTERED HASH (o_id, od_id) WITH (BUCKET_COUNT = 10000)  
)  
WITH (MEMORY_OPTIMIZED = ON)  
  
 SELECT p_id  
 FROM dbo.od  
 WHERE o_id=1  
```  
  
 该表在两列 (o_id, od_id) 上具有哈希索引，而查询在 (o_id) 上具有相等谓词。 因为该查询仅在索引键列的子集上具有相等谓词，所以，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不能使用 PK_od 执行索引查找操作；[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 而是必须恢复到全文索引扫描。  
  
 **解决方法：** 有多种可能的解决方法。 例如：  
  
-   将索引作为非聚集类型而不是非聚集哈希重新创建。 内存优化的非聚集索引是有序的，因此，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可对前导索引键列执行索引查找。 该示例最后生成的主键定义将是 `constraint PK_od primary key nonclustered`。  
  
-   更改当前索引键以便匹配 WHERE 子句中的列。  
  
-   添加与查询的 WHERE 子句中的列匹配的新哈希索引。 在该示例中，最后生成的表定义将如下所示：  
  
    ```tsql  
    CREATE TABLE dbo.od  
     ( o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
  
     CONSTRAINT PK_od PRIMARY KEY   
     NONCLUSTERED HASH (o_id,od_id) WITH (BUCKET_COUNT=10000),  
  
     INDEX ix_o_id NONCLUSTERED HASH (o_id) WITH (BUCKET_COUNT=10000)  
  
     ) WITH (MEMORY_OPTIMIZED=ON)  
    ```  
  
 请注意，如果对于某一给定的索引键值存在许多重复行，则内存优化的哈希索引不会达到最佳性能：在该示例中，如果针对 o_id 列的唯一值的数目远小于该表中的行数，则在 (o_id) 上添加索引并非最佳选择；将索引 index PK_od 的类型从哈希更改为非聚集应该是更好的解决方法。 有关详细信息，请参阅[哈希索引确定正确的存储桶计数](../relational-databases/indexes/indexes.md)。  
  
## <a name="see-also"></a>请参阅  
 [内存优化表上的索引](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
