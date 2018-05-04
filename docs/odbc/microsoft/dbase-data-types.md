---
title: dBASE 数据类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44d057bb934469270e4ff87d9c21997ff7408054
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="dbase-data-types"></a>dBASE 数据类型
下表显示如何 dBASE 数据类型映射到 ODBC SQL 数据类型。 请注意，并非所有 ODBC SQL 数据类型都受都支持。  
  
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
  
 精度中 dBASE III 允许的数字向上到两位数指数，在 dBASE IV 数字与最大为三位数指数。 由于的数字以文本形式存储，则它们会转换为数字。 如果要转换的数字不适合在字段中，可能会出现无法解释的结果。  
  
 虽然 dBASE 使精度和小数位数指定数值数据类型，它不支持 ODBC dBASE 驱动程序。 ODBC dBASE 驱动程序始终返回 15 精度和小数位数为 0 表示数值数据类型。  
  
 创建与使用 ODBC dBASE 驱动程序映射到 SQL_DOUBLE ODBC 数据类型的数值数据类型的列。 因此，此列中的数据是容易产生舍入。 此行为是不相同作为的数值数据中的类型 dBASE （类型为 N），它是二进制编码的十进制 (BCD)。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC SQL 数据类型。 附录 D 中的所有转换*ODBC 程序员参考*支持本主题前面列出的 ODBC SQL 数据类型。  
  
 下表显示限制上 dBASE 数据类型。  
  
|数据类型|Description|  
|---------------|-----------------|  
|CHAR|创建零 CHAR 列或未指定的长度实际返回 254 字节的列。|  
|加密数据|DBASE 驱动程序不支持加密的 dBASE 表。|  
|逻辑|DBASE 驱动程序无法在逻辑列上创建索引。|  
|备注|MEMO 列的最大长度为 65500 字节。|  
  
 了解更多限制对数据类型可在[数据类型限制](../../odbc/microsoft/data-type-limitations.md)。
