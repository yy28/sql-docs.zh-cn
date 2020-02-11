---
title: 表名限制 |Microsoft Docs
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
ms.openlocfilehash: 152a0aa1e8d92424b2f60c49f44888de7d3e528c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67939778"
---
# <a name="table-name-limitations"></a>表名称限制
表名可以包含任何有效字符（例如，空格）。 如果表名包含除字母、数字和下划线之外的任何字符，则必须用引号（'）将该名称括起来。  
  
 当使用 Microsoft Excel 驱动程序时，如果数据库引用不限定表名，则默认数据库是隐含的。 如果 Microsoft Excel 中的某个名称包含 "！" 字符，则它将自动转换为 "$" 字符。  
  
 Microsoft Excel 3.0 和4.0 文件支持\<引用 filename> 的 microsoft excel 表名称。 Microsoft Excel 5.0、7.0 或 97 \<文件支持引用工作簿名称> 的 microsoft excel 表名称。  
  
 使用 dBASE 驱动程序时，将 ASCII 值大于127的字符转换为下划线。  
  
 使用 Microsoft Access 驱动程序时，表名称限制为64个字符。  
  
 使用 dBASE、Microsoft Excel 3.0 或4.0、Paradox 或文本驱动程序时，不应将特殊的 MS-DOS 关键字 CON、AUX、LPT1 和 LPT2 用作表名称。
