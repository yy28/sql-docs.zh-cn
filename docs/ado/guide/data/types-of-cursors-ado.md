---
title: 类型的游标 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db77de95e83e596a8a301fa65885ee640c742a71
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472309"
---
# <a name="types-of-cursors-ado"></a>游标类型 (ADO)
作为一般规则，你的应用程序应使用的最简单的游标的提供所需的数据访问。 每个只进、 只读、 静态、 滚动 （无缓冲） 的基础知识以外的其他游标特征具有价格-在客户端内存、 网络负载或性能。 在许多情况下，默认游标选项生成更复杂的游标不是应用程序实际需要。  
  
 所选的游标类型取决于你的应用程序如何使用结果集和也几个设计注意事项，包括大小的结果集，可能会使用的数据的百分比、 数据更改和应用程序性能的敏感度系统要求。  
  
 最起码，光标选择取决于您是否需要更改或只需查看的数据：  
  
-   如果只需要滚动浏览一系列的结果，但不是更改数据，使用[只进](../../../ado/guide/data/forward-only-cursors.md)或[静态](../../../ado/guide/data/static-cursors.md)游标。  
  
-   如果你有较大的结果集并且需要选择只需几行，使用[由键集](../../../ado/guide/data/keyset-cursors.md)游标。  
  
-   如果你想要同步的结果集与最新添加、 更改，并删除所有的并发用户，请使用[动态](../../../ado/guide/data/dynamic-cursors.md)游标。  
  
 尽管每种游标类型看起来不同，但请注意，这些游标类型不是这么多不同类型作为只是重叠的特征和选项的结果。  
  
 本部分包含以下主题。  
  
-   [只进游标](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [静态游标](../../../ado/guide/data/static-cursors.md)  
  
-   [键集游标](../../../ado/guide/data/keyset-cursors.md)  
  
-   [动态游标](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>请参阅  
 [只进游标](../../../ado/guide/data/forward-only-cursors.md)   
 [静态游标](../../../ado/guide/data/static-cursors.md)   
 [由键集游标](../../../ado/guide/data/keyset-cursors.md)   
 [动态游标](../../../ado/guide/data/dynamic-cursors.md)
