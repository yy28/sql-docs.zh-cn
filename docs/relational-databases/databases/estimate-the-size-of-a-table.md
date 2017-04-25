---
title: "估计表的大小 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pages [SQL Server], space
- space [SQL Server], tables
- row size [SQL Server]
- size [SQL Server], tables
- column size [SQL Server]
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- disk space [SQL Server], tables
- space allocation [SQL Server], table size
- designing databases [SQL Server], estimating size
- reserved free rows per page [SQL Server]
- calculating table size
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 740800db335b524298c39a3ab9f225e18d785c54
ms.lasthandoff: 04/11/2017

---
# <a name="estimate-the-size-of-a-table"></a>估计表的大小
  可以使用下列步骤估计在表中存储数据所需的空间：  
  
1.  按照 [估计堆的大小](../../relational-databases/databases/estimate-the-size-of-a-heap.md) 或 [估计聚集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)中的说明来计算堆或聚集索引所需空间。  
  
2.  对于每个非聚集索引，按照 [估计非聚集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)中的说明来计算其所需空间。  
  
3.  对步骤 1 和步骤 2 中计算的值求和。  
  
## <a name="see-also"></a>另请参阅  
 [估计数据库的大小](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [估计堆的大小](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [估计聚集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [估计非聚集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  
