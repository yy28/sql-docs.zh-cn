---
title: 列名称限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14e62555db2e88c6573f3bdca0d4a1a2733d428b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006246"
---
# <a name="column-name-limitations"></a>列名限制
列名称可以包含任何有效的字符 （例如，空格）。 如果列名称中包含除字母、 数字和下划线的任何字符，必须由括在单引号 （'）） 后分隔名称。  
  
 使用 Microsoft Access 或 Microsoft Excel 驱动程序时，列名称限制为 64 个字符，并且较长的名称生成一个错误。 当使用 Paradox 驱动程序时，最大列名称是 25 个字符。 使用文本驱动程序时，最大列名称是 64 个字符，并且较长的名称会被截断。  
  
 当使用 dBASE 驱动程序时，使用 ASCII 值大于 127 的字符都转换为下划线。  
  
 使用 Microsoft Excel 驱动程序时，如果列名已存在，则他们必须位于第一行。 名称将使用在 Microsoft Excel 中的"！"字符必须括在单引号 （'）） 后。 "！"字符被转换为"$"字符，因为"！"字符不是法律中一个 ODBC 的名称，即使该名称用引号括起来后。 所有其他有效的 Microsoft Excel 字符 (除非管道字符 (&#124;)) 可在列名称，包括空格。 分隔的标识符必须用于 Microsoft Excel 列名称包含空格。 未指定的列名称将替换驱动程序生成的名称，例如，"Col1"的第一列。  
  
 竖线字符 (&#124;) 指示名称是否用后的引号或不列名称，不能用于。  
  
 使用文本驱动程序时，该驱动程序提供一个默认名称如果未指定列名称。 例如，驱动程序调用的第一列 F1，第二个列 F2，依此类推。
