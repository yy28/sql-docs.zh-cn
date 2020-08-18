---
description: 对齐方式
title: 对齐 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alignment issues [ODBC]
ms.assetid: 06a01e51-e7a5-495f-aa27-e304b0d005ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1402eee289111ca100e80730d8df4a6d0e3299cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483140"
---
# <a name="alignment"></a>对齐方式
ODBC 应用程序中的对齐问题通常与其他任何应用程序中的对齐问题都没有区别。 也就是说，大多数 ODBC 应用程序的对齐方式都很少或没有问题。 不对齐地址的惩罚会因硬件和操作系统而异，并且可能会略微降低性能或严重运行时错误。 因此，ODBC 应用程序（尤其是可移植的 ODBC 应用程序）应小心地正确对齐数据。  
  
 ODBC 应用程序遇到对齐问题的一个示例是在分配大量内存块时，将内存的不同部分绑定到结果集中的列。 当一般应用程序必须在运行时确定结果集的形状，并相应地分配和绑定内存时，最有可能发生这种情况。  
  
 例如，假设某个应用程序执行用户输入的 **SELECT** 语句，并从此语句获取结果。 由于编写程序时此结果集的形状未知，因此，应用程序必须在创建结果集后确定每个列的类型并相应地绑定内存。 要执行此操作，最简单的方法是分配一个较大的内存块并将该块中的不同地址绑定到每个列。 若要访问列中的数据，应用程序会将绑定的内存强制转换为该列。  
  
 下图显示了一个示例结果集，以及如何使用每个 SQL 数据类型的默认 C 数据类型将内存块绑定到该结果集。 每个 "X" 表示一个字节的内存。  (此示例只显示绑定到列的数据缓冲区。 这是为了简单起见。 在实际的代码中，长度/指示器缓冲区还必须对齐。 )   
  
 ![默认情况下将 C 数据类型绑定到 SQL 数据类型](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 假设绑定地址存储在 *地址* 数组中，则应用程序使用以下表达式访问绑定到每个列的内存：  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 请注意，绑定到第二列和第三列的地址将以奇数个字节开始，并且绑定到第三列的地址不能被四整除，这是 SDWORD 的大小。 在某些计算机上，这不是问题;在其他情况下，这会导致轻微的性能损失;在其他情况下，它将导致严重运行时错误。 更好的解决方案是在其自然对齐边界上对齐每个绑定地址。 假设这对于 UCHAR 为1，2表示剑，4表示 SDWORD，这将提供下图所示的结果，其中，"X" 表示所使用的内存量，而 "O" 表示未使用的内存量。  
  
 ![按自然对齐边界绑定](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 虽然此解决方案不使用应用程序的所有内存，但它不会遇到任何对齐问题。 遗憾的是，它需要大量代码来实现此解决方案，因为每列都必须按照其类型进行单独对齐。 更简单的解决方案是在最大对齐边界的大小上对齐所有列，在下图中显示的示例中为4。  
  
 ![按最大对齐边界绑定](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 尽管此解决方案会留下更大的洞，但实现此方案的代码相对简单快捷。 在大多数情况下，这会抵消未使用内存中支付的处罚。 有关使用此方法的示例，请参阅 [Using SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。
