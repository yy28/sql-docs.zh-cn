---
title: 在记录集中移动到更多方式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: acc9da7f07836d0aad8e9cc60a79ff117371dd46
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822615"
---
# <a name="more-ways-to-move-in-a-recordset"></a>在记录集中移动的更多方法
以下四种方法可用来四处移动，或向下滚动，在**记录集**: [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)。 （某些的这些方法不能对只进游标。）  
  
 **MoveFirst**更改为中的第一个记录的记录当前位置**记录集**。 **MoveLast**中记录的更改的当前记录的最后一个定位**记录集**。 若要使用**MoveFirst**或**MoveLast**，则**记录集**对象必须支持书签或向后的光标的移动; 否则为方法调用将生成错误。  
  
 **MoveNext**移动当前记录向前定位一个位置。 如果您是在最后一个记录时调用**MoveNext**， **EOF**将设置为**True**。 **MovePrevious**移动当前记录位置向后的一个位置。 如果您是上第一条记录时，调用**MovePrevious**， **BOF**将设置为**True**。 最好检查**EOF**和**BOF**属性时使用这些方法并将光标移回至有效的当前记录位置移出的任一端如果**记录集**，如下所示：  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 或者的情况下**MovePrevious**方法：  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 在情况下，**记录集**已筛选或排序和当前记录的数据发生更改时，还可更改位置。 在这种情况下**MoveNext**方法仍正常工作，但请注意位于移动的一个正向记录从新位置，而不是旧位置。 例如，更改当前记录中的数据，以便该记录移到末尾的已排序**记录集**，就意味着，调用**MoveNext**在 ADO 中设置为当前记录结果中的最后一个记录之后的位置**记录集**(**EOF** = **True**)。  
  
 各种迁移方法的行为**记录集**对象中的数据在某种程度上依赖**记录集**。 新记录添加到**记录集**最初添加按特定顺序，这由数据源定义，并且可能依赖于隐式或显式的新记录中的数据。 例如，如果一种或联接中完成填充的查询**记录集**，将在相应位置内插入新记录**记录集**。 如果排序未显式指定在创建时**记录集**，数据源实现中的更改可能会在无意中更改所返回行的排序。 在添加、 排序、 筛选和编辑的功能**记录集**可以影响顺序和可能是可见的记录集中的行。  
  
 因此， **MoveNext**， **MovePrevious**， **MoveFirst**， **MoveLast**，并**移动**同时在同一个执行其他操作不区分**记录集**。 ADO 将始终尝试保持当前的位置，直到你显式移动它，但有时，干扰更改使其难以理解的后续移动效果。 例如，如果您调用**MoveFirst**到上一个经过排序的第一行的位置**记录集**并且从升序和降序排序更改排序，则仍在同一行上，但现在它是最后一行在中**记录集**。 **MoveFirst**将转到不同的行 （新的第一行）。  
  
 再举一例，如果你位于特定行的中间**记录集**并调用**删除**，然后调用**MoveNext**，你现在位于记录紧跟已删除的记录。 但调用**MovePrevious**使前一删除当前记录，因为已删除的记录不会再计数中的有效的成员资格的记录**记录集**。  
  
 它是特别难移动相对于当前记录的方法的所有提供程序定义一致移动语义 — **MovePrevious**， **MoveNext**，和**移动** — 在面对变化的当前记录中的数据。 例如，如果您正在使用一个经过排序，筛选**记录集**，和你更改当前记录中的数据，以便它将位于之前所有其他记录，但已更改的数据也不再与该筛选器匹配，不清楚的位置**MoveNext**操作执行。 最安全的结论是中的相对移动**记录集**是风险是否高于绝对移动 (例如，使用**MoveFirst**或**MoveLast**) 数据时更改而正在编辑的记录，添加或删除。 排序和筛选应基于 primary key 或 ID，因为此类型的值不应更改。
