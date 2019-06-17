---
title: SQLColAttributes 映射 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], mapping
ms.assetid: 30e25719-176b-4c48-97d4-920766b22412
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7a1508d10431ba9975c44a2002faa4e5b913312
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199405"
---
# <a name="sqlcolattributes-mapping"></a>SQLColAttributes 映射
当应用程序调用**SQLColAttributes**通过 ODBC 3 *.x*驱动程序，将会调用**SQLColAttributes**映射到**SQLColAttribute** ，如下所示：  
  
> [!NOTE]
>  在中使用的前缀*FieldIdentifier* ODBC 3 中的值 *.x*已从该中使用的 ODBC 2。*x*。 新的前缀为"SQL_DESC";旧的前缀为"SQL_COLUMN"。  
  
1.  如果应用程序的 ODBC 2。*x*应用程序中， *fDescType*为 SQL_COLUMN_TYPE，且返回的类型为简明的日期时间类型，返回值的日期、 时间和时间戳的代码的驱动程序管理器映射。  
  
2.  如果*fDescType* SQL_COLUMN_NAME、 SQL_COLUMN_NULLABLE，或 SQL_COLUMN_COUNT，驱动程序管理器调用**SQLColAttribute**中使用的驱动程序*FieldIdentifier*参数映射到 SQL_DESC_NAME、 SQL_DESC_NULLABLE 或 SQL_DESC_COUNT，根据需要 *。* 所有其他值的*fDescType*传递到驱动程序。  
  
 ODBC 3 *.x*驱动程序必须支持所有 ODBC 3 *.x* *FieldIdentifiers*列出**SQLColAttribute**。  
  
 ODBC 3 *.x* SQL_COLUMN_PRECISION 和 SQL_DESC_PRECISION、 SQL_COLUMN_SCALE 和 SQL_DESC_SCALE，和 SQL_COLUMN_LENGTH 和 SQL_DESC_LENGTH 驱动程序必须支持。 这些值则不同，因为精度、 小数位数和长度定义以不同的方式在 ODBC 3 *.x*比 ODBC 2 中。*x*。 有关详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)中附录 d:数据类型。
