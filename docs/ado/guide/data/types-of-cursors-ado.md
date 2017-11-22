---
title: "类型的游标 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c8ab039bfe5754587e3f7adda36c0b715138d65
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="types-of-cursors-ado"></a>类型的游标 (ADO)
作为一般规则，你的应用程序应使用的最简单的光标，提供所需的数据访问。 （只进、 只读的、 静态、 滚动、 未缓冲） 的基础知识以外的每个其他游标特征都有价格-在客户端内存、 网络负载或性能。 在许多情况下，默认游标选项生成的更复杂的游标不是你的应用程序则实际上需要。  
  
 你选择的游标类型取决于你的应用程序如何使用结果集并且也将在多个设计注意事项，其中包括的结果集，可能会使用的数据的百分比、 数据更改和应用程序性能的敏感性大小要求。  
  
 在其最基本的你光标选择取决于是否需要更改或只需查看的数据：  
  
-   如果你只需浏览的结果，而不是更改数据集，使用[只进](../../../ado/guide/data/forward-only-cursors.md)或[静态](../../../ado/guide/data/static-cursors.md)光标。  
  
-   如果你有大型结果集和需要选择只需几行，使用[键集](../../../ado/guide/data/keyset-cursors.md)光标。  
  
-   如果你想要同步的结果集与最近添加、 更改，并通过所有的并发用户中删除，请使用[动态](../../../ado/guide/data/dynamic-cursors.md)光标。  
  
 尽管每种游标类型看起来需不同，但请注意，这些游标类型不是更不同类型作为只需重叠的特征和选项的结果。  
  
 本部分包含以下主题。  
  
-   [只进游标](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [静态游标](../../../ado/guide/data/static-cursors.md)  
  
-   [键集游标](../../../ado/guide/data/keyset-cursors.md)  
  
-   [动态游标](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>另请参阅  
 [只进游标](../../../ado/guide/data/forward-only-cursors.md)   
 [静态游标](../../../ado/guide/data/static-cursors.md)   
 [键集游标](../../../ado/guide/data/keyset-cursors.md)   
 [动态游标](../../../ado/guide/data/dynamic-cursors.md)
