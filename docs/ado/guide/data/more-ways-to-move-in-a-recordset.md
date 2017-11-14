---
title: "在记录集中移动到更多方式 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c3e3f666fd96a1b00d78ba364a8df062fa3f6397
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="more-ways-to-move-in-a-recordset"></a>在记录集中移动到更多的方法
以下四个方法用于解决问题，移动或向下滚动，在**记录集**: [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)。 （其中的某些方法是在只进游标中不可用）。  
  
 **MoveFirst**更改为中的第一个记录的当前记录位置**记录集**。 **MoveLast**当前记录到最后一个位置的更改记录在**记录集**。 若要使用**MoveFirst**或**MoveLast**、**记录集**对象必须支持书签或向后的光标移动; 否则，该方法调用将生成错误。  
  
 **MoveNext**移动当前记录向前定位一个位置。 如果要在最后一个记录当调用**MoveNext**， **EOF**将设置为**True**。 **MovePrevious**移动当前记录的位置向后的一个位置。 如果您是上第一条记录时你调用**MovePrevious**， **BOF**将设置为**True**。 若要检查明智的做法是**EOF**和**BOF**属性时使用这些方法和在需要时移动光标返回到有效的当前记录位置移开的任意一端**记录集**，如下所示：  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 或者，对于**MovePrevious**方法：  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 在情况下其中**记录集**已筛选或排序，而且更改当前记录的数据，也可能更改位置。 在这种情况下**MoveNext**方法仍正常工作，但请注意位于移动的一个转发记录从新位置，而不是旧位置。 例如，更改当前记录中的数据，以便记录移到末尾的排序**记录集**，意味着该调用**MoveNext**导致 ADO 将当前记录设置为位置中的最后一个记录后**记录集**(**EOF** = **True**)。  
  
 行为的各种移动方法**记录集**对象在某种程度上，对内的数据依赖**记录集**。 新记录添加到**记录集**最初添加按特定顺序，由数据源定义，并可能依赖隐式或显式的新记录中的数据。 例如，如果一个排序，或联接完成了填充查询内**记录集**，将在中的适当位置插入新记录**记录集**。 如果未指定排序则显式创建时**记录集**，数据源实现中的更改可能导致无意中更改返回的行的排序。 在添加、 排序、 筛选和编辑功能的**记录集**可以影响顺序和记录集的行可能将可见。  
  
 因此， **MoveNext**， **MovePrevious**， **MoveFirst**， **MoveLast**，和**移动**全部在相同上执行其他操作的区分**记录集**。 ADO 将始终尝试保持当前的位置，除非您显式移动它，但有时，中间更改将很难了解后续移动的效果。 例如，如果你调用**MoveFirst**到上一个经过排序的第一行的位置**记录集**并且从升序和降序更改排序，则仍在同一行上，但现在它的最后一行在**记录集**。 **MoveFirst**将转到不同的行 （新的第一行）。  
  
 再举一例，如果您处在之中的特定行上**记录集**并且你调用**删除**，然后调用**MoveNext**，现在，你可以对记录紧跟在已删除的记录。 但调用**MovePrevious**使之前删除了当前的记录，因为已删除的记录不会再计数的活动成员资格方面的记录**记录集**。  
  
 很特别难移动相对于当前记录的方法的所有提供程序定义一致移动语义- **MovePrevious**， **MoveNext**，和**移动** — 在面对变化的当前记录中的数据。 例如，如果你正在使用一个经过排序，筛选**记录集**，和你更改当前记录中的数据，以便它将位于之前所有其他记录，但已更改的数据也不再与筛选器匹配，不清楚的位置**MoveNext**你应执行操作。 最安全的结论也在此相对移动**记录集**是风险比绝对移动 (例如，使用**MoveFirst**或**MoveLast**) 数据时更改时编辑了记录，添加或删除。 排序和筛选应基于的主键或 ID，因为此类型的值不应更改。

