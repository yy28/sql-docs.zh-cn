---
title: Microsoft Excel 数据类型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10695dd9bf044e270bb1ce1d26de78e53a1dd85a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656755"
---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel 数据类型
下表显示了如何将 Microsoft Excel 驱动程序数据类型映射到 ODBC SQL 数据类型。 Microsoft Excel 驱动程序将这些数据类型分配给基于列中的数据在 Microsoft Excel 表中的列。  
  
|Microsoft Excel 数据类型|ODBC 数据类型|  
|-------------------------------|--------------------|  
|货币|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|逻辑|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC SQL 数据类型。 所有转换中的附录 D *ODBC 程序员参考*支持本主题中前面列出的 ODBC SQL 数据类型。  
  
 下表显示有关 Microsoft Excel 数据类型的限制。  
  
|数据类型|Description|  
|---------------|-----------------|  
|加密数据|Microsoft Excel 驱动程序无法读取加密的数据。|  
|错误字符串|Microsoft Excel 驱动程序不能返回字符串的 Microsoft Excel 错误值 (# n/A ！，#VALUE ！，#REF ！，#DIV/0 ！，#NUM ！，#NAME？，和 #NULL ！)，但改为返回 NULL。|  
|逻辑|SQL_C_CHAR 缓冲区中返回逻辑列中的值为 0 或 1。|  
|NUMBER|如果创建了一个整数列，输入对整数数据类型来说太大的数字，并且可以插入包含非整数值的数据与列可能被转换为 SQL_DOUBLE 结果。|  
|TEXT|当列的行包含多个 Microsoft Excel 数据类型时，ODBC Microsoft Excel 驱动程序将 SQL_VARCHAR 数据类型分配给列。 还有一个例外： 如果该列包含只有两个或三个日期时间数据类型 （日期、 时间和日期时间），ODBC Microsoft Excel 驱动程序将 SQL_TIMESTAMP 数据类型分配给列。<br /><br /> 创建文本列的零或未指定的长度实际上返回一个 255 字节的列。<br /><br /> 字符的字符串文本可以包含任何 ANSI 字符 （1-255 十进制）。 使用两个连续单引号 （'） 来表示一个单引号 （'）。<br /><br /> 将 NULL 插入列 SQL_VARCHAR 之外的数据类型将导致列更改为 SQL_VARCHAR 数据类型。|  
  
 了解更多限制，对数据类型可在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)。
