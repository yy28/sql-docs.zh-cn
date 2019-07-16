---
title: 对齐方式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b8b5a107f5ed8cd1c6c45317e60cc515a2601316
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077268"
---
# <a name="alignment"></a>对齐方式
通常没有什么不同比任何其他应用程序是在 ODBC 应用程序中的对齐问题。 也就是说，大多数 ODBC 应用程序具有弱或根本没有问题的对齐方式。 用于不对齐地址损失因硬件和操作系统，可能是作为对略微的性能产生负面影响等小或为主要作为运行时错误。 因此，ODBC 应用程序和可移植的 ODBC 应用程序具体而言，应务必正确对齐的数据。  
  
 一个 ODBC 应用程序时遇到对齐问题的示例是当它们分配大的内存块并将该内存的不同部分绑定到结果集中的列。 这是最有可能发生时通用的应用程序必须在运行时确定的结果集的形状和分配并相应地绑定内存。  
  
 例如，假设应用程序执行**选择**语句由用户输入并通过此语句提取结果。 因为此结果集的形状不知道编写程序时，应用程序必须确定每个列的类型，创建结果集之后，并相应地绑定内存。 若要执行此操作的最简单方法是内存的分配大块并将该块中的不同的地址绑定到每个列。 若要访问某一列中的数据，应用程序将绑定到该列的内存强制转换。  
  
 下图显示示例结果集和可能为每个 SQL 数据类型使用默认 C 数据类型与其绑定的内存块的方式。 每个"X"表示单字节的内存。 （此示例演示了绑定到列的数据缓冲区。 这是为了简单起见。 在实际代码中，长度/指示器缓冲区必须也在对齐。）  
  
 ![绑定到 SQL 数据类型的默认 C 数据类型](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 假设的绑定的地址存储在*地址*数组，该应用程序使用以下表达式访问绑定到每个列的内存：  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 请注意，地址绑定到第二个和第三个列一开始是对奇数个字节，该地址绑定到第三列不可被由 4 个，这是 SDWORD 的大小。 在某些计算机上，这不会是一个问题：对于其他项目，它将导致对略微的性能产生负面影响;对于仍其他项目，它将导致运行时错误。 更好的解决方案是将每个绑定的地址其自然对齐边界上对齐。 假设这 SWORD 的 2 和 4 为 SDWORD UCHAR 的 1，这可能使显示在下图中，其中"X"表示使用的内存字节的"O"表示的是未使用的内存字节的结果。  
  
 ![按自然对齐边界绑定](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 此解决方案不使用的所有应用程序的内存，而没有遇到任何问题。 遗憾的是，它需要大量的代码来实现此解决方案中，按每个列都必须根据其类型单独对齐方式。 更简单的解决方案是对齐的大小为 4 的最大对齐边界上的所有列中如下图中所示的示例。  
  
 ![按最大对齐边界绑定](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 尽管此解决方案使更大的漏洞，实现它的代码是相对简单且快速。 在大多数情况下，此偏移量中未使用的内存付费的损失。 使用此方法的示例，请参阅[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。
