---
title: "对齐方式 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- alignment issues [ODBC]
ms.assetid: 06a01e51-e7a5-495f-aa27-e304b0d005ff
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 412c04f8181997738bac1fc7b457c9ec0c3efcde
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="alignment"></a>Alignment
ODBC 应用程序中的对齐方式问题并通常没有什么区别不是它们处于任何其他应用程序。 这就是，大多数 ODBC 应用程序具有带对齐方式的弱或根本没有问题。 因为不对齐地址受到处罚硬件和操作系统而异，并且可能导致性能略微下降作为等小或为主要视为致命的运行时错误。 因此，ODBC 应用程序和可移植的 ODBC 应用程序尤其是，应小心地将其正确对齐的数据。  
  
 一个 ODBC 应用程序时遇到对齐问题的示例是当它们分配大的内存块，并将该内存的不同部分绑定到结果集中的列。 这是最有可能通用的应用程序必须在运行时确定的结果集的形状和分配以及相应地绑定内存时出现。  
  
 例如，假设应用程序执行**选择**语句由用户输入，并通过此语句获取结果。 因为此结果集的形状不知道何时写入程序，应用程序必须确定每个列的类型，创建结果集后，相应地绑定内存。 若要执行此操作的最简单方法是内存的分配大块，并将该块中的不同地址绑定到每个列。 若要访问某一列中的数据，应用程序，请将绑定到该列的内存。  
  
 下图显示示例结果设置以及如何的内存块可能绑定到它为每个 SQL 数据类型使用默认 C 数据类型。 每个"X"表示单字节的内存。 （此示例显示绑定到的列的数据缓冲区。 为简单起见完成此操作。 在实际代码中，长度/指示器缓冲区必须还对齐。）  
  
 ![默认为 SQL 数据类型的 C 数据类型由绑定](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 假设绑定的地址存储在*地址*数组，应用程序使用以下表达式访问绑定到每个列的内存：  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 请注意，地址绑定到第二个和第三个列在奇数字节上启动的地址绑定到第三列不是由 4 个，即 SDWORD 大小整除。 在某些计算机上此将不会有问题;对于其他项目，它将导致性能略微下降;对于仍其他项目，它将导致运行时错误。 更好的解决方案将对齐其自然对齐边界上的每个绑定的地址。 假设这 1 个用于 UCHAR，双刃剑 2 和 4 SDWORD，这会使下图中，其中"X"表示使用内存的字节，"O"表示一字节的未使用的内存中所示的结果。  
  
 ![绑定由自然对齐边界](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 尽管此解决方案不使用的所有应用程序的内存，它不会遇到对齐方式的任何问题。 遗憾的是，它采用大量代码来实现此解决方案，按每个列都必须根据其类型单独对齐方式。 更简单的解决方案是将所有列的大小为 4 的最大对齐边界上都对齐在下图中显示的示例。  
  
 ![按最大对齐边界绑定](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 尽管此解决方案离开更大的漏洞，来实现它的代码是相对较简单和快速。 在大多数情况下，此偏移量付费中未使用的内存的损失。 使用此方法的示例，请参阅[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。

