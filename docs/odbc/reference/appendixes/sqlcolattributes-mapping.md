---
title: SQLColattributes 映射 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c2c8386d6771141eaa0145a5d5964d70d6084d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305413"
---
# <a name="sqlcolattributes-mapping"></a>SQLColAttributes 映射
当应用程序通过 ODBC *3.x*驱动程序调用**SQLColAttributes**时，对**SQLColAttributes**的调用将映射到**SQLColAttribute，** 如下所示：  
  
> [!NOTE]
>  ODBC *3.x*中*字段标识符*值中使用的前缀已更改，与 ODBC *2.x*中使用的前缀相比。 新前缀为"SQL_DESC";新前缀为"SQL_DESC";如果 "SQL_DESC"，则为"SQL_DESC"旧前缀为"SQL_COLUMN"。  
  
1.  如果应用程序是 ODBC *2.x*应用程序，*则 fDescType*是SQL_COLUMN_TYPE，并且返回的类型是简洁的 DATETIME 类型，则驱动程序管理器映射日期、时间和时间戳代码的返回值。  
  
2.  如果*fDescType*是SQL_COLUMN_NAME、SQL_COLUMN_NULLABLE 或SQL_COLUMN_COUNT，则驱动程序管理器在驱动程序中调用**SQLColAttribute，** 并根据需要将*字段标识符*参数映射到SQL_DESC_NAME、SQL_DESC_NULLABLE或*SQL_DESC_COUNT。* *fDescType*的所有其他值都传递给驱动程序。  
  
 ODBC *3.x*驱动程序必须支持为**SQLColAttribute**列出的所有 ODBC *3.x* *字段标识符*。  
  
 ODBC *3.x*驱动程序必须支持SQL_COLUMN_PRECISION和SQL_DESC_PRECISION、SQL_COLUMN_SCALE和SQL_DESC_SCALE以及SQL_COLUMN_LENGTH和SQL_DESC_LENGTH。 这些值不同，因为在 ODBC *3.x*中定义的精度、比例和长度与 ODBC *2.x*中的定义不同。 有关详细信息，请参阅附录 D 中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)：数据类型。
