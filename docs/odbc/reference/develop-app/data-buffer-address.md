---
title: 数据缓冲区地址 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f07f835361fcf29143376fe468a55f0bf26e31e3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471126"
---
# <a name="data-buffer-address"></a>数据缓冲区地址
应用程序将数据缓冲区的地址传递给在参数中，通常名为驱动程序*ValuePtr*或类似名称。 例如，在下面的示例调用到**SQLBindCol**，应用程序指定的地址*日期*变量：  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 如中所述[Allocating 和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)部分中，延迟的缓冲区的地址必须保持有效，直到取消绑定此缓冲区。  
  
 除非明确禁止，否则数据缓冲区的地址可以是 null 指针。 对于用来将数据发送到该驱动程序的缓冲区，这会导致驱动程序忽略通常包含在缓冲区中的信息。 对于用来从驱动程序中检索数据的缓冲区，这会导致驱动程序不返回值。 在这两种情况下，该驱动程序将忽略相应的数据缓冲区长度参数。
