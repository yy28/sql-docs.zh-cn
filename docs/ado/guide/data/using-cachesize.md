---
title: 使用 CacheSize |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d0b6a1b83b09d504f8f3394a32ee10d556fcd18c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699736"
---
# <a name="using-cachesize"></a>使用 CacheSize
使用**CacheSize**属性来控制要在一次检索到本地内存中从提供程序记录数。 例如，如果**CacheSize**为 10，第一个打开之后**记录集**对象，该提供程序检索到本地内存前 10 条记录。 当你移动通过**记录集**对象，该提供程序返回的数据从本地内存缓冲区。 一旦您跳过缓存中的最后一个记录，该提供程序会将接下来 10 条记录从数据源检索到缓存。  
  
> [!NOTE]
>  **CacheSize**基于**最大打开行**提供程序特定属性 (在**属性**集合**记录集**对象)。 不能设置**CacheSize**的值大于**打开的最大行数。** 若要修改的提供程序可以打开的行数，请设置**最大打开行**。  
  
 值**CacheSize**进行调整的生命周期内**记录集**对象，但更改此值仅在数据源中的后续检索后影响缓存中的记录数。 更改属性值本身不会更改当前缓存的内容。  
  
 如果有较少的记录检索比**CacheSize**指定提供程序返回其余记录，而不会出现错误。  
  
 一个**CacheSize**零设置不允许，将返回错误。  
  
 从缓存中检索的记录不反映其他用户对源数据的并发更改。 若要强制进行所有缓存数据的更新，请使用[重新同步](../../../ado/reference/ado-api/resync-method.md)方法。  
  
 如果**CacheSize**设置为值大于 1，导航方法 ([移动](../../../ado/reference/ado-api/move-method-ado.md)， [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) 可能会导致导航到已删除如果删除操作发生后检索到的记录的，记录。 后初始提取时，后续的删除操作将不会反映在数据缓存之前尝试访问从已删除行的数据值。 但是，将设置**CacheSize**因为不能提取已删除的行，则为 1 消除此问题。
