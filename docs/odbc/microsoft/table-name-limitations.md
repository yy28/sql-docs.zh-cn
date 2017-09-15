---
title: "表名称限制 |Microsoft 文档"
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
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 690b6242b9e8d38b6a1f26ddbd823215030e2b15
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="table-name-limitations"></a>表名称的限制
表名称可以包含任何有效字符 （例如，空格）。 如果表名称包含除字母、 数字和下划线的任何字符，必须由将其括起来后引号 （'） 中分隔名称。  
  
 在使用 Microsoft Excel 驱动程序，并且由数据库引用不限定表名，则会进行隐式的默认数据库。 如果在 Microsoft Excel 中的名称包含"！"字符，它将自动将其转换为"$"字符相反。  
  
 引用的 Microsoft Excel 表名称\<文件名 > 支持 Microsoft Excel 3.0 和 4.0 的文件。 引用的 Microsoft Excel 表名称\<工作薄名称 > 的 Microsoft Excel 5.0、 7.0 或 97 文件支持。  
  
 当使用 dBASE 驱动程序时，与 ASCII 值大于 127 个字符将转换为下划线。  
  
 当使用 Microsoft Access 驱动程序时，表名称被限制为 64 个字符。  
  
 当使用 dBASE，Microsoft Excel 3.0 或 4.0，Paradox 或文本驱动程序时，特殊 MS-DOS 关键字 CON、 AUX、 LPT1，和 LPT2 应不用作表名。
