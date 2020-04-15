---
title: 对齐 |微软文档
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
ms.openlocfilehash: 205cc3ff95dd60db215150f46ae894fbb99bd9ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288602"
---
# <a name="alignment"></a>Alignment
ODBC 应用程序中的对齐问题通常与任何其他应用程序中的对齐问题没有什么不同。 也就是说，大多数 ODBC 应用程序在对齐方面几乎没有问题或没有问题。 不对齐地址的处罚与硬件和操作系统不同，可能很小，如轻微的性能损失或主要作为致命的运行时错误。 因此，ODBC 应用程序，特别是便携式 ODBC 应用程序，应小心正确对齐数据。  
  
 当 ODBC 应用程序遇到对齐问题时，一个例子是，当它们分配一大块内存并将该内存的不同部分绑定到结果集中的列时。 当泛型应用程序必须在运行时确定结果集的形状并相应地分配和绑定内存时，最有可能发生这种情况。  
  
 例如，假设应用程序执行用户输入的**SELECT**语句并从该语句中获取结果。 由于编写程序时不知道此结果集的形状，因此应用程序必须在创建结果集后确定每列的类型并相应地绑定内存。 最简单的方法是分配一个大内存块，并将该块中的不同地址绑定到每列。 要访问列中的数据，应用程序将强制转换绑定到该列的内存。  
  
 下图显示了示例结果集，以及如何使用每个 SQL 数据类型的默认 C 数据类型将其绑定到它。 每个"X"表示内存的单个字节。 （此示例仅显示绑定到列的数据缓冲区。 这样做是为了简单起见。 在实际代码中，长度/指示器缓冲区也必须对齐。  
  
 ![默认情况下将 C 数据类型绑定到 SQL 数据类型](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 假设绑定地址存储在*Address*数组中，则应用程序使用以下表达式访问绑定到每列的内存：  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 请注意，绑定到第二列和第三列的地址以奇数字节开头，并且绑定到第三列的地址不能被四个整除，即 SDWORD 的大小。 在某些计算机上，这不是问题;因此，这将成为问题。对他人，将造成轻微的绩效处罚;在其他人上，它会导致致命的运行时错误。 更好的解决方案是对齐其自然对齐边界上的每个绑定地址。 假设 UCHAR 为 1，SWORD 为 2，SDWORD 为 4，则给出下图所示的结果，其中"X"表示使用的内存字节，"O"表示未使用的内存字节。  
  
 ![按自然对齐边界绑定](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 虽然此解决方案不使用应用程序的所有内存，但它不会遇到任何对齐问题。 遗憾的是，实现此解决方案需要大量代码，因为每列必须根据其类型单独对齐。 更简单的解决方案是对齐最大对齐边界大小上的所有列，如下图所示示例中为 4。  
  
 ![按最大对齐边界绑定](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 尽管此解决方案留下了较大的漏洞，但实现它的代码相对简单且快速。 在大多数情况下，这抵消了在未使用的内存中支付的罚款。 有关使用此方法的示例，请参阅[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。
