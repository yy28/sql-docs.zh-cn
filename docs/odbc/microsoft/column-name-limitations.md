---
title: 列名称限制 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7d51f87a2fbb3552dd323469d60bd50c7bab7f22
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="column-name-limitations"></a>列名称限制
列名称可以包含任何有效字符 （例如，空格）。 如果列名包含除字母、 数字和下划线的任何字符，必须由将其括起来后引号 （'） 中分隔名称。  
  
 当使用 Microsoft Access 或 Microsoft Excel 驱动程序时，列名称限制为 64 个字符，并且较长的名称生成错误。 当使用 Paradox 驱动程序时，最大的列名称将为 25 个字符。 当使用文本驱动程序时，最大的列名称为 64 个字符，并且较长的名称会被截断。  
  
 当使用 dBASE 驱动程序时，与 ASCII 值大于 127 个字符将转换为下划线。  
  
 当使用 Microsoft Excel 驱动程序时，列名称是否存在时，则它们必须在第一行。 名称在 Microsoft Excel 中将使用"！"字符必须括在后引号 （'）。 "！"字符被转换为"$"字符，因为"！"字符不是合法中 ODBC 名称，即使该名称括在后引号。 所有其他有效的 Microsoft Excel 字符 (除非竖线字符 (&#124;)) 可在列名称，包括空格。 分隔的标识符必须用于 Microsoft Excel 列名称包含空格。 未指定的列名称将替换驱动程序生成的名称，例如，"Col1"的第一列。  
  
 管道字符 (&#124;) 不能在列名称，是否名称用引号括起来后与否。  
  
 当使用文本驱动程序时，该驱动程序将提供一个默认名称，如果未指定列名称。 例如，该驱动程序调用的第一列 F1，第二列 F2，依次类推。
