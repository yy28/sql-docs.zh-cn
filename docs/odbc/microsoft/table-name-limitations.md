---
title: 表名称限制 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 738c563961eae56471f0238d9726a1ebb0bdc76e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289213"
---
# <a name="table-name-limitations"></a>表名称限制
表名称可以包含任何有效的字符（例如空格）。 如果表名称包含除字母、数字和下划线以外的任何字符，则必须通过在后引号 （'） 中括起来来分隔名称。  
  
 当使用 Microsoft Excel 驱动程序，并且数据库引用不限定表名称时，隐含默认数据库。 如果 Microsoft Excel 中的名称包含"！"字符，则该名称将自动转换为"$"字符。  
  
 Microsoft Excel 3.0\<和 4.0 文件支持引用文件名>的 Microsoft Excel 表名。 Microsoft Excel 5.0、7.0 或 97 个文件支持引用\<工作簿名称>的 Microsoft Excel 表名称。  
  
 使用 dBASE 驱动程序时，ASCII 值大于 127 的字符将转换为下划线。  
  
 使用 Microsoft Access 驱动程序时，表名称限制为 64 个字符。  
  
 当使用 dBASE、Microsoft Excel 3.0 或 4.0、Paradox 或文本驱动程序时，不应将特殊的 MS-DOS 关键字 CON、AUX、LPT1 和 LPT2 用作表名。
