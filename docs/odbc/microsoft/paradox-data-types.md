---
title: Paradox 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8478e80ae2ebd19a3e0f2aa8307e0985b2c092d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043687"
---
# <a name="paradox-data-types"></a>Paradox 数据类型
ODBC Paradox 驱动程序将 Paradox 数据类型映射为 ODBC SQL 数据类型。 下表列出了所有 Paradox 数据类型，并显示数据类型映射到的 ODBC SQL。  
  
|Paradox 数据类型|ODBC 数据类型|  
|-----------------------|--------------------|  
|字母数字|SQL_VARCHAR|  
|AUTOINCREMENT [1]|SQL_INTEGER|  
|BCD[1]|SQL_DOUBLE|  
|BYTES[1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|IMAGE[2]|SQL_LONGVARBINARY|  
|LOGICAL[1]|SQL_BIT|  
|长时间 [1]|SQL_INTEGER|  
|备注 [2]|SQL_LONGVARCHAR|  
|MONEY[1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|短|SQL_SMALLINT|  
|TIME[1]|SQL_TIMESTAMP|  
|TIMESTAMP[1]|SQL_TIMESTAMP|  
  
 [1] 适用于仅 Paradox 版本 5。*x*。  
  
 只有特定的 Paradox 版本 4 的 [2] 有效。*x*和 5。*x*。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC SQL 数据类型。 所有转换中的附录 D *ODBC 程序员参考*支持本主题中前面列出的 ODBC SQL 数据类型。  
  
 下表显示有关 Paradox 数据类型的限制。  
  
|数据类型|描述|  
|---------------|-----------------|  
|字母数字|创建零的字母数字列或未指定的长度实际上返回一个 255 字节的列。|  
|BYTES|如果您具有 Paradox5 驱动程序的二进制列中插入 NULL，则将它更改为 0。|  
|LONG|Paradox 5 中的长整型数据类型的 Paradox 驱动程序支持的最大负值。*x*不为-2 ^31 (-2147483648)，也应如此长映射到 ODBC 数据以来键入 SQL_INTEGER。 支持长时间的最大负值为实际上-2 ^31 + 1 (在-2147483647)。|  
|timestamp|当由 Paradox 驱动程序插入到 TIMESTAMP 列则随后从列中检索一个值时，检索到的值可能不同于插入的值由多达 1 秒由于舍入。|  
  
 了解更多限制，对数据类型可在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)。
