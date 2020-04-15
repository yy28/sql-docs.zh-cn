---
title: 微软Excel数据类型 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8574985e10e5aaa3ae5431af7ee1245643e20b60
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283767"
---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel 数据类型
下表显示了如何将 Microsoft Excel 驱动程序数据类型映射到 ODBC SQL 数据类型。 Microsoft Excel 驱动程序根据列中的数据将这些数据类型分配给 Microsoft Excel 表中的列。  
  
|微软 Excel 数据类型|ODBC 数据类型|  
|-------------------------------|--------------------|  
|货币|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|逻辑|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC SQL 数据类型。 本主题前面列出的 ODBC SQL 数据类型都支持*ODBC 程序员参考*附录 D 中的所有转换。  
  
 下表显示了对 Microsoft Excel 数据类型的限制。  
  
|数据类型|描述|  
|---------------|-----------------|  
|加密数据|Microsoft Excel 驱动程序无法读取加密数据。|  
|错误字符串|Microsoft Excel 驱动程序无法返回 Microsoft Excel 错误值（#N/A！、#VALUE！、#REF！、#DIV/0！、#NUM！、#NAME 和 #NULL！）的字符串，而是返回 NULL。|  
|逻辑|"逻辑"列中的值在SQL_C_CHAR缓冲区中返回为 0 或 1。|  
|NUMBER|如果创建了整数列，则可以输入对于整数数据类型太大的数字，并可以插入包含非整数值的数据，结果该列可以转换为SQL_DOUBLE。|  
|TEXT|当列的行包含多个 Microsoft Excel 数据类型时，ODBC Microsoft Excel 驱动程序会将SQL_VARCHAR数据类型分配给该列。 存在一个例外：如果列仅包含两个或三个日期时间数据类型（日期、时间和 DATETIME），则 ODBC Microsoft Excel 驱动程序将SQL_TIMESTAMP数据类型分配给列。<br /><br /> 创建零或未指定长度的 TEXT 列实际上返回 255 字节列。<br /><br /> 字符串文本可以包含任何 ANSI 字符（1-255 位小数）。 使用两个连续的单引号 （"） 表示一个单引号 （'）。<br /><br /> 将 NULL 插入具有SQL_VARCHAR以外的数据类型的列将导致列的数据类型更改为SQL_VARCHAR。|  
  
 数据类型的更多限制可以在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)中找到。
