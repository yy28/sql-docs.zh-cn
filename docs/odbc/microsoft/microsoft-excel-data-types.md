---
title: "Microsoft Excel 数据类型 |Microsoft 文档"
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
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eeb2bc72ce34141eb3dbdca3f952dca0c476c2dd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel 数据类型
下表显示如何将 Microsoft Excel 驱动程序数据类型映射到 ODBC SQL 数据类型。 Microsoft Excel 驱动程序将这些数据类型分配给基于列中的数据的 Microsoft Excel 表中的列。  
  
|Microsoft Excel 数据类型|ODBC 数据类型|  
|-------------------------------|--------------------|  
|货币|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|逻辑|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC SQL 数据类型。 附录 D 中的所有转换*ODBC 程序员参考*支持本主题前面列出的 ODBC SQL 数据类型。  
  
 下表显示了有关 Microsoft Excel 数据类型的限制。  
  
|数据类型|Description|  
|---------------|-----------------|  
|加密数据|Microsoft Excel 驱动程序无法读取加密的数据。|  
|错误字符串|Microsoft Excel 驱动程序不能返回 Microsoft Excel 错误值的字符字符串 (# n/A ！，#VALUE ！，#REF ！，#DIV/0 ！，#NUM ！，#NAME？，和 #NULL ！)，但改为将返回 NULL。|  
|逻辑|SQL_C_CHAR 缓冲区中返回逻辑列中的值为 0 或 1。|  
|NUMBER|如果创建一个整数列，则可以输入的数字，则对整数数据类型来说太大，并可以使用结果列可能被转换为 SQL_DOUBLE 情况，插入包含非整数值的数据。|  
|TEXT|如果一列的行包含多个 Microsoft Excel 数据类型，ODBC Microsoft Excel 驱动程序会将 SQL_VARCHAR 数据类型分配给列。 没有一个例外： 如果列包含仅两个或三个日期时间数据类型 （日期、 时间和日期时间），ODBC Microsoft Excel 驱动程序将 SQL_TIMESTAMP 数据类型分配给列。<br /><br /> 创建文本列的零或未指定的长度实际返回 255 字节的列。<br /><br /> 字符的字符串文本可以包含任何 ANSI 字符 （1-255 个十进制）。 使用两个连续单引号 （'） 来表示一个单引号 （'）。<br /><br /> 将 NULL 插入列与数据类型不是 SQL_VARCHAR 将导致要将更改为 SQL_VARCHAR 的列的数据类型。|  
  
 了解更多限制对数据类型可在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)。

