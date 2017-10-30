---
title: "相对和绝对滚动 |Microsoft 文档"
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
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cf5155a44827adb972881da17ac2bc05d92a0cd4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="relative-and-absolute-scrolling"></a>相对和绝对滚动
中的滚动选项大多数**SQLFetchScroll**将光标位置相对于当前的位置或位置的绝对位置。 **SQLFetchScroll**支持提取下一行，之前，第一个和最后一个行集，作为很好地为相对提取 (提取行集* n *从开始的当前行集的行) 和绝对提取 (提取从行开始的行集* n *)。 如果* n *是中的绝对读取负，行进行计数从结果集的末尾。 因此，行为-1 的绝对读取意味着提取开头结果集中的最后一行的行集。  
  
 动态游标检测行插入和删除从结果集中，因此没有为动态游标来检索从结果集，这可能非常缓慢的开头处以外读取特定数量的行的轻松方法。 此外，绝对提取不是在动态游标中非常有用因为行号更改随着行的插入和删除;因此，连续提取相同的行数可以产生不同的行。  
  
 应用程序使用**SQLFetchScroll**仅为其块光标功能，如报表，可能会将结果集通过一次仅选项用于提取下一步的行集。 基于屏幕的应用程序，另一方面，可以充分利用所有功能的**SQLFetchScroll**。 如果应用程序将行集大小设置为在屏幕上显示的行数，并将屏幕缓冲区绑定到结果集，它可以转换滚动栏操作直接调用**SQLFetchScroll**。  
  
|滚动条操作|SQLFetchScroll 滚动选项|  
|--------------------------|-------------------------------------|  
|向上翻页|SQL_FETCH_PRIOR|  
|向下翻页|SQL_FETCH_NEXT|  
|向上移动一行|与 SQL_FETCH_RELATIVE *FetchOffset*等于 – 1|  
|向下移动一行|与 SQL_FETCH_RELATIVE *FetchOffset*等于 1|  
|在顶部的滚动框|SQL_FETCH_FIRST|  
|在底部的滚动框|SQL_FETCH_LAST|  
|滚动框位于随机位置|SQL_FETCH_ABSOLUTE|  
  
 此类应用程序还需要放置滚动操作之后，它要求的当前行号和的行数的滚动条。 当前行号，应用程序可以是跟踪的当前行号或调用**SQLGetStmtAttr**具有 SQL_ATTR_ROW_NUMBER 属性来检索该值。  
  
 游标，这是结果的大小中的行数设置，则将用作诊断标头的 SQL_DIAG_CURSOR_ROW_COUNT 字段。 此字段中的值定义之后才**SQLExecute**， **SQLExecDirect**，或**SQLMoreResult**已调用。 此计数可以的近似计数或进行确切计数，具体取决于驱动程序的功能。 可以通过调用确定驱动程序的支持**SQLGetInfo**游标属性的信息类型和检查是否针对的游标类型返回 SQL_CA2_CRC_APPROXIMATE 或 SQL_CA2_CRC_EXACT 位。  
  
 对于动态游标从不支持的确切的行计数。 对于其他类型的游标，该驱动程序可以支持准确或近似行计数，但不是两者。 如果驱动程序支持既不准确，也不大致行计数为特定的游标类型、 SQL_DIAG_CURSOR_ROW_COUNT 字段包含到目前为止已提取的行数。 无论何种驱动程序支持， **SQLFetchScroll**与*操作*的 SQL_FETCH_LAST 将导致 SQL_DIAG_CURSOR_ROW_COUNT 字段包含的确切的行计数。

