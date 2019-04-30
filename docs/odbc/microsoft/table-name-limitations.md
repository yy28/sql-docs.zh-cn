---
title: 表名称限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31c1703bc03a2881e7b9b96989b8949cc81aba7b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63226348"
---
# <a name="table-name-limitations"></a>表名称限制
表名可以包含任何有效的字符 （例如，空格）。 如果表名称中包含除字母、 数字和下划线的任何字符，必须由括在单引号 （'）） 后分隔名称。  
  
 当使用 Microsoft Excel 驱动程序，并由数据库引用不限定表名时，则暗指的默认数据库。 如果在 Microsoft Excel 中的名称包含"！"字符，它都将自动转换为"$"字符相反。  
  
 引用的 Microsoft Excel 表名\<文件名 > 支持适用于 Microsoft Excel 3.0 和 4.0 的文件。 引用的 Microsoft Excel 表名\<工作簿名称 > 的 Microsoft Excel 5.0、 7.0、 或 97 文件支持。  
  
 当使用 dBASE 驱动程序时，使用 ASCII 值大于 127 的字符都转换为下划线。  
  
 使用 Microsoft Access 驱动程序时，表名称限于 64 个字符。  
  
 当使用 dBASE，Microsoft Excel 3.0 或 4.0，Paradox 或文本驱动程序时，特殊 MS-DOS 关键字 CON、 AUX、 LPT1，和 LPT2 应不用作表名。
