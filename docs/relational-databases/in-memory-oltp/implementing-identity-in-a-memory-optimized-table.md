---
title: "在内存优化表中实现 IDENTITY | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 21133ec5172c13b5d010c9aef1f461282acd35b5
ms.lasthandoff: 04/11/2017

---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>在内存优化的表中实现 IDENTITY
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

只要种子和增量值均为 1（即默认值），那么内存优化表就支持 IDENTITY。 内存优化表不支持使用 IDENTITY(x, y)（其中 x != 1 或 y != 1 ）定义的标识列。   
    
若要增加 IDENTITY 种子，使用会话选项 `SET IDENTITY_INSERT table_name ON`为标识列插入具有显式值的新行。 插入该行后，IDENTITY 种子将更改为显式插入的值加上 1。 例如，若要将种子的值增加到 1000，在标识列中插入值为 999 的行。 生成的标识值便就将从 1000 开始。     
  
## <a name="see-also"></a>另请参阅  
 [迁移到内存中 OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
