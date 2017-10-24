---
title: "使用 CacheSize |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 74ec85c5907485edc5ad8dbcb6c24826fc21ccf3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-cachesize"></a>使用 CacheSize
使用**CacheSize**属性控制将在一次检索到从提供程序的本地内存的记录数。 例如，如果**CacheSize**后第一个左为 10，**记录集**对象，该提供程序检索前 10 条记录到本地内存。 当你移动通过**记录集**对象，该提供程序从本地内存缓冲区中返回数据。 一旦移过缓存中的最后一个记录，即会将提供程序会将从数据源的接下来的 10 的记录检索到缓存中。  
  
> [!NOTE]
>  **CacheSize**基于**打开的最大行数**提供程序特定属性 (在**属性**集合**记录集**对象)。 无法设置**CacheSize**为值大于**打开的最大行数。** 若要修改的提供程序可以打开的行数，设置**打开的最大行数**。  
  
 值**CacheSize**进行调整的生命周期内**记录集**对象，但更改此值仅影响在缓存中的记录数后的后续检索的数据源。 更改属性值本身不会更改当前缓存的内容。  
  
 如果没有较少的记录，可供检索比**CacheSize**指定，该提供程序返回剩下的记录，且不发生错误。  
  
 A **CacheSize**设置为零时不允许，并返回错误。  
  
 从缓存中检索的记录不能反映其他用户对源数据所做的并发更改。 若要强制执行更新的所有缓存的数据，使用[重新同步](../../../ado/reference/ado-api/resync-method.md)方法。  
  
 如果**CacheSize**设置为值大于 1，浏览方法 ([移动](../../../ado/reference/ado-api/move-method-ado.md)， [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) 可能会导致导航到已删除如果已检索的记录后，将发生删除，记录。 后初始提取，后续的删除将不会反映在你的数据缓存之前尝试访问从已删除的行的数据值。 但是，将设置**CacheSize**由于无法提取已删除的行，则为 1 消除此问题。

