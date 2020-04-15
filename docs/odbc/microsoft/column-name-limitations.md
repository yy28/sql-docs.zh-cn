---
title: 列名称限制 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 41d973afdac360af114da41620997cad23a2c740
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281377"
---
# <a name="column-name-limitations"></a>列名限制
列名称可以包含任何有效的字符（例如空格）。 如果列名称包含除字母、数字和下划线以外的任何字符，则必须通过在后引号 （'） 中括起来来分隔名称。  
  
 使用 Microsoft Access 或 Microsoft Excel 驱动程序时，列名限制为 64 个字符，较长的名称将生成错误。 使用悖论驱动程序时，最大列名称为 25 个字符。 使用 Text 驱动程序时，最大列名称为 64 个字符，并截断较长的名称。  
  
 使用 dBASE 驱动程序时，ASCII 值大于 127 的字符将转换为下划线。  
  
 使用 Microsoft Excel 驱动程序时，如果存在列名称，它们必须位于第一行中。 Microsoft Excel 中将使用"！" 字符的名称必须包含在后引号 （'） 中。 "！" 字符转换为"$"字符，因为"！ 所有其他有效的 Microsoft Excel 字符（管道字符（&#124;）除外）都可以在列名称中使用，包括空格。 必须为 Microsoft Excel 列名称使用分隔标识符才能包含空格。 未指定的列名称将替换为驱动程序生成的名称，例如，第一列的"Col1"。  
  
 无论名称是否包含在后引号中，都不能在列名称中使用管道字符 （&#124;）。  
  
 使用 Text 驱动程序时，如果未指定列名称，则驱动程序提供默认名称。 例如，驱动程序调用第一列 F1、第二列 F2 等。
