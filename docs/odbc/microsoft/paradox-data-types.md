---
title: "Paradox 数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e63f642f7a1921f9d65cd6f8fe665b9e83c9404c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="paradox-data-types"></a>Paradox 数据类型
ODBC Paradox 驱动程序将 Paradox 数据类型映射到 ODBC SQL 数据类型。 下表列出了所有 Paradox 数据类型，并显示它们映射到的数据类型的 ODBC SQL。  
  
|Paradox 数据类型|ODBC 数据类型|  
|-----------------------|--------------------|  
|字母数字|SQL_VARCHAR|  
|AUTOINCREMENT [1]|SQL_INTEGER|  
|BCD [1]|SQL_DOUBLE|  
|字节 [1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|映像 [2]|SQL_LONGVARBINARY|  
|逻辑 [1]|SQL_BIT|  
|LONG 类型的值 [1]|SQL_INTEGER|  
|备注 [2]|SQL_LONGVARCHAR|  
|MONEY [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|短|SQL_SMALLINT|  
|时间 [1]|SQL_TIMESTAMP|  
|时间戳 [1]|SQL_TIMESTAMP|  
  
 仅对 Paradox 版本 5 的 [1] 有效。*x*。  
  
 仅对 Paradox 版本 4 的 [2] 有效。*x*和 5。*x*。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC SQL 数据类型。 附录 D 中的所有转换*ODBC 程序员参考*支持本主题前面列出的 ODBC SQL 数据类型。  
  
 下表显示了有关 Paradox 数据类型的限制。  
  
|数据类型|Description|  
|---------------|-----------------|  
|字母数字|创建零的字母数字列或未指定的长度实际返回 255 字节的列。|  
|BYTES|如果使用 Paradox5 驱动程序二进制列中插入 NULL，则将它更改为 0。|  
|LONG|Paradox 5 中的长整型数据类型可能是驱动程序支持最大负值。*x*不是-2 ^31 (-2147483648)，也应该是因为长映射到 ODBC 数据键入 SQL_INTEGER。 支持长时间的最大负数的值是实际-2 ^31 + 1 (在-2147483647)。|  
|timestamp|当值插入时间戳列 Paradox 驱动程序，则随后从该列检索时，检索到的值可能不同于插入的值由多达 1 秒由于舍入。|  
  
 了解更多限制对数据类型可在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)。
