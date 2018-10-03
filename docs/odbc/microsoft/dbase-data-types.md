---
title: dBASE 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc4b4c7a5c1074a62bf0e84d265840109f65ea55
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626265"
---
# <a name="dbase-data-types"></a>dBASE 数据类型
下表显示了如何将 dBASE 数据类型映射到 ODBC SQL 数据类型。 请注意，并非所有 ODBC SQL 数据类型都支持。  
  
|dBASE 数据类型|ODBC 数据类型|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT [1]|SQL_DOUBLE|  
|逻辑|SQL_BIT|  
|备注|SQL_LONGVARCHAR|  
|数字 (BCD)|SQL_DOUBLE|  
|OLEOBJECT [1]|SQL_LONGBINARY|  
  
 仅为 dBASE 版本 5 的的 [1] 有效。*x*  
  
 精度 dBASE III 允许数字向上两位数指数，在 dBASE IV 数字与最多三个数字指数的后面。 数字以文本形式存储，因为它们会转换为数字。 如果要转换的数字不适合在字段中，可能会发生无法解释的结果。  
  
 尽管 dBASE 允许精度和小数位数指定数值数据类型，它不是支持 ODBC dBASE 驱动程序。 ODBC dBASE 驱动程序始终返回 15 的精度和小数位数为 0 的数值数据类型。  
  
 创建与使用 ODBC dBASE 驱动程序映射到 ODBC SQL_DOUBLE 数据类型的数值数据类型的列。 因此，此列中的数据是四舍五入的值。 此行为不是相同的数值数据类型中 dBASE （类型为 N），这是二进制编码的十进制 (BCD)。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC SQL 数据类型。 所有转换中的附录 D *ODBC 程序员参考*支持本主题中前面列出的 ODBC SQL 数据类型。  
  
 下表显示限制上 dBASE 数据类型。  
  
|数据类型|Description|  
|---------------|-----------------|  
|CHAR|创建零对 CHAR 列或未指定的长度实际上返回一个 254 字节的列。|  
|加密数据|DBASE 驱动程序不支持加密的 dBASE 表。|  
|逻辑|DBASE 驱动程序不能逻辑列创建索引。|  
|备注|备注列的最大长度为 65,500 个字节。|  
  
 了解更多限制，对数据类型可在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)。
