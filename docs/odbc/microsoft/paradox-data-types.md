---
title: 悖论数据类型 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a85cf643a6d22b9b2fce15984539d74dc43c62ab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290927"
---
# <a name="paradox-data-types"></a>Paradox 数据类型
ODBC 悖论驱动程序将悖论数据类型映射到 ODBC SQL 数据类型。 下表列出了所有 Paradox 数据类型，并显示了映射到的 ODBC SQL 数据类型。  
  
|悖论数据类型|ODBC 数据类型|  
|-----------------------|--------------------|  
|字母|SQL_VARCHAR|  
|自动递增[1]|SQL_INTEGER|  
|BCD[1]|SQL_DOUBLE|  
|字节[1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|图片[2]|SQL_LONGVARBINARY|  
|逻辑[1]|SQL_BIT|  
|长[1]|SQL_INTEGER|  
|备忘录[2]|SQL_LONGVARCHAR|  
|钱[1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|SHORT|SQL_SMALLINT|  
|时间[1]|SQL_TIMESTAMP|  
|时间戳[1]|SQL_TIMESTAMP|  
  
 [1] 仅适用于悖论版本 5。*x*. .  
  
 [2] 仅适用于悖论版本 4。*x*和 5。*x*. .  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC SQL 数据类型。 本主题前面列出的 ODBC SQL 数据类型都支持*ODBC 程序员参考*附录 D 中的所有转换。  
  
 下表显示了对悖论数据类型的限制。  
  
|数据类型|描述|  
|---------------|-----------------|  
|字母|创建零或未指定长度的 ALPHA 数字列实际上返回 255 字节列。|  
|BYTES|如果将 NULL 插入具有 Paradox5 驱动程序的二进制列中，则它将更改为 0。|  
|LONG|悖论 5 中长数据类型的悖论驱动程序支持的最大负值。*x*不是 -2^31 （-2147483648），因为它应该是因为长映射到 ODBC 数据类型SQL_INTEGER。 Long 支持的最大负值实际上是 -2^31 = 1 （-2147483647）。|  
|TIMESTAMP|当一个值被 Paradox 驱动程序插入到 TIMESTAMP 列中，然后从该列检索时，检索的值可能与插入的值相差 1 秒，因为舍入。|  
  
 数据类型的更多限制可以在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)中找到。
