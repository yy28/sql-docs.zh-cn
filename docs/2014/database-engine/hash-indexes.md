---
title: 哈希索引 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f4bdc9c1-7922-4fac-8183-d11ec58fec4e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 263fdcd4b09c4acc6c2bba4d67629f867d64c6b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779477"
---
# <a name="hash-indexes"></a>哈希索引
  索引用作内存优化表的入口点。 从表读取行需要借助索引在内存中定位数据。  
  
 哈希索引包含以数组形式组织的 Bucket 集合。 哈希函数将索引键映射到哈希索引中对应的 Bucket。 下图展示映射到哈希索引中三个不同 Bucket 的三个索引键。 出于演示目的，哈希函数的名称为 f(x)。  
  
 ![索引键映射到不同 bucket。](../../2014/database-engine/media/hekaton-tables-2.gif "索引键映射到不同 bucket。")  
  
 用于哈希索引的哈希函数具有以下特征：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 拥有一个用于所有哈希索引的哈希函数。  
  
-   哈希函数具有确定性。 同一索引键始终映射到哈希索引中的同一 Bucket。  
  
-   多个索引键可能映射到同一个哈希 Bucket。  
  
-   哈希函数经过均衡处理，这意味着索引键值在哈希桶上的分布通常符合泊松分布。  
  
     泊松分布并非均匀分布。 索引键值并非均匀地分布在哈希 Bucket中。 例如，泊松分布*n*个不同索引键转移*n*哈希存储桶中大约三分之一的空 bucket，三分之一的 bucket 包含一个索引键和其他第三个结果包含两个索引键。 少量 Bucket 将包含两个以上的键。  
  
 如果两个索引键映射到同一个哈希 Bucket，则产生哈希冲突。 大量哈希冲突可影响读取操作的性能。  
  
 内存哈希索引结构包含一个内存指针数组。 每个 Bucket 映射到该数组中的一个偏移位置。 数组中的每个 Bucket 指向该哈希 Bucket 中的第一行。 Bucket 中的每行指向下行，因而形成了每个哈希 Bucket 的行链，如下图所示。  
  
 ![内存中哈希索引结构。](../../2014/database-engine/media/hekaton-tables-3.gif "内存中哈希索引结构。")  
  
 该图有三个包含行的 Bucket。 顶部的第二个 Bucket 包含三个红色行。 第四个 Bucket 包含一个蓝色行。 底部的 Bucket 包含两个绿色行。 这些可能是同一行的不同版本。  
  
 有关内存优化表的索引的详细信息，请参阅[在内存优化表上使用索引的准则](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
## <a name="see-also"></a>请参阅  
 [内存优化表上的索引](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  
