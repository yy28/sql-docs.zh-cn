---
title: "数据缓冲地址 |Microsoft 文档"
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
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7d57b8ec52324dd4bec320b6179507ab3102e629
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="data-buffer-address"></a>数据缓冲区地址
应用程序将数据缓冲区的地址传递给自变量，通常名为中的驱动程序*ValuePtr*或类似的名称。 例如，在下面的示例调用**SQLBindCol**，应用程序将指定的地址*日期*变量：  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 中所述[Allocating 和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)部分中，延迟的缓冲区的地址必须保持有效，直到缓冲区是未绑定。  
  
 除非专门禁止，数据缓冲区的地址可以是 null 指针。 对于将数据发送到该驱动程序所使用的缓冲，这会导致要忽略通常包含在缓冲区中的信息的驱动程序。 对于用来从驱动程序检索数据的缓冲区，这会导致驱动程序不返回值。 在这两种情况下，该驱动程序将忽略相应的数据缓冲区长度自变量。
