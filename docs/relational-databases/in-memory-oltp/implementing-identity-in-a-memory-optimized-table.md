---
title: "在内存优化表中实现 IDENTITY | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9bb5c976841d7b249a3c3d0a72e1ba661ca0a64c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>在内存优化的表中实现 IDENTITY
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

只要种子和增量值均为 1（即默认值），那么内存优化表就支持 IDENTITY。 内存优化表不支持使用 IDENTITY(x, y)（其中 x != 1 或 y != 1 ）定义的标识列。   
    
若要增加 IDENTITY 种子，使用会话选项 `SET IDENTITY_INSERT table_name ON`为标识列插入具有显式值的新行。 插入该行后，IDENTITY 种子将更改为显式插入的值加上 1。 例如，若要将种子的值增加到 1000，在标识列中插入值为 999 的行。 生成的标识值便就将从 1000 开始。     
  
## <a name="see-also"></a>另请参阅  
 [迁移到内存中 OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
