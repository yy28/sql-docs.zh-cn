---
title: 在内存优化表中实现 IDENTITY | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 375804e451429a90a2031c72f4909e3b7a468a2d
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>在内存优化的表中实现 IDENTITY
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

只要种子和增量值均为 1（即默认值），那么内存优化表就支持 IDENTITY。 内存优化表不支持使用 IDENTITY(x, y)（其中 x != 1 或 y != 1 ）定义的标识列。   
    
若要增加 IDENTITY 种子，使用会话选项 `SET IDENTITY_INSERT table_name ON`为标识列插入具有显式值的新行。 插入该行后，IDENTITY 种子将更改为显式插入的值加上 1。 例如，若要将种子的值增加到 1000，在标识列中插入值为 999 的行。 生成的标识值便就将从 1000 开始。     
  
## <a name="see-also"></a>另请参阅  
 [迁移到内存中 OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
