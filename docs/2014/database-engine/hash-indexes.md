---
title: 哈希索引 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f4bdc9c1-7922-4fac-8183-d11ec58fec4e
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 3da74688d6a2f65b191788ab9ecd2394bcca8597
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028860"
---
# <a name="hash-indexes"></a>哈希索引
  索引用作内存优化表的入口点。 从表读取行需要借助索引在内存中定位数据。  
  
 哈希索引包含以数组形式组织的 Bucket 集合。 哈希函数将索引键映射到哈希索引中对应的 Bucket。 下图展示映射到哈希索引中三个不同 Bucket 的三个索引键。 出于演示目的，哈希函数的名称为 f(x)。  
  
 ![索引键映射到不同的存储桶。](../../2014/database-engine/media/hekaton-tables-2.gif "索引键映射到不同的存储桶。")  
  
 用于哈希索引的哈希函数具有以下特征：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 拥有一个用于所有哈希索引的哈希函数。  
  
-   哈希函数具有确定性。 同一索引键始终映射到哈希索引中的同一 Bucket。  
  
-   多个索引键可能映射到同一个哈希 Bucket。  
  
-   哈希函数经过均衡处理，这意味着索引键值在哈希桶上的分布通常符合泊松分布。  
  
     泊松分布并非均匀分布。 索引键值并非均匀地分布在哈希 Bucket中。 例如，泊松分布的*n*非重复索引键通过*n*哈希桶中约三分之一空存储桶，包含一个索引键和其他第三个存储桶的三分之一的结果包含两个索引键。 少量 Bucket 将包含两个以上的键。  
  
 如果两个索引键映射到同一个哈希 Bucket，则产生哈希冲突。 大量哈希冲突可影响读取操作的性能。  
  
 内存哈希索引结构包含一个内存指针数组。 每个 Bucket 映射到该数组中的一个偏移位置。 数组中的每个 Bucket 指向该哈希 Bucket 中的第一行。 Bucket 中的每行指向下行，因而形成了每个哈希 Bucket 的行链，如下图所示。  
  
 ![内存中哈希索引结构。](../../2014/database-engine/media/hekaton-tables-3.gif "内存中哈希索引结构。")  
  
 该图有三个包含行的 Bucket。 顶部的第二个 Bucket 包含三个红色行。 第四个 Bucket 包含一个蓝色行。 底部的 Bucket 包含两个绿色行。 这些可能是同一行的不同版本。  
  
 有关内存优化表的索引的详细信息，请参阅[对于使用内存优化表的索引的指导原则](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
## <a name="see-also"></a>请参阅  
 [内存优化表上的索引](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  