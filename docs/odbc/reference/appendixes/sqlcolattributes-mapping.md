---
title: "SQLColAttributes 映射 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], mapping
ms.assetid: 30e25719-176b-4c48-97d4-920766b22412
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d21d1a9a9565ad2c0accbebb716d0b24f18f854d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattributes-mapping"></a>SQLColAttributes 映射
在应用程序调用**SQLColAttributes**到 ODBC 3*.x*驱动程序，将会调用**SQLColAttributes**映射到**SQLColAttribute** ，如下所示：  
  
> [!NOTE]  
>  中使用的前缀*FieldIdentifier* ODBC 3 中的值*.x*已从该中使用 ODBC 2。*x*。 新的前缀为"SQL_DESC";旧的前缀为"SQL_COLUMN"。  
  
1.  如果应用程序是 ODBC 2。*x*应用程序， *fDescType* SQL_COLUMN_TYPE，并返回的类型是简洁的 DATETIME 类型，返回值的日期、 时间和时间戳的代码的驱动程序管理器映射。  
  
2.  如果*fDescType*是 SQL_COLUMN_NAME、 SQL_COLUMN_NULLABLE，还是 SQL_COLUMN_COUNT，驱动程序管理器调用**SQLColAttribute**与驱动程序中*FieldIdentifier*自变量映射到 SQL_DESC_NAME、 SQL_DESC_NULLABLE 或 SQL_DESC_COUNT，根据*。* 所有其他值*fDescType*传递到该驱动程序。  
  
 ODBC 3*.x*驱动程序必须支持所有 ODBC 3*.x* *FieldIdentifiers*列出**SQLColAttribute**。  
  
 ODBC 3*.x*驱动程序必须支持 SQL_COLUMN_PRECISION 和 SQL_DESC_PRECISION、 SQL_COLUMN_SCALE 和 SQL_DESC_SCALE，和 SQL_COLUMN_LENGTH 和 SQL_DESC_LENGTH。 这些值会不同，因为精度、 小数位数和长度定义以不同方式在 ODBC 3*.x* ODBC 2 中相比。*x*。 有关详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。

