---
description: 列名限制
title: 列名限制 |Microsoft Docs
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
ms.openlocfilehash: 82cac260fc81ce5a2cfbbe3e4c3c0bdab5a47049
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483690"
---
# <a name="column-name-limitations"></a>列名限制
列名称可以包含任何有效的字符 (例如，空格) 。 如果列名包含除字母、数字和下划线之外的任何字符，则必须用引号将该名称括起来 (") 。  
  
 使用 Microsoft Access 或 Microsoft Excel 驱动程序时，列名称限制为64个字符，更长的名称会生成错误。 使用 Paradox 驱动程序时，最大列名称为25个字符。 使用文本驱动程序时，最大列名称为64个字符，更长的名称将被截断。  
  
 使用 dBASE 驱动程序时，将 ASCII 值大于127的字符转换为下划线。  
  
 使用 Microsoft Excel 驱动程序时，如果列名称存在，则它们必须位于第一行。 Microsoft Excel 中使用 "！" 字符的名称必须用反引号 (") 括起来。 "！" 字符转换为 "$" 字符，因为 "！" 字符在 ODBC 名称中是非法的，即使该名称括在引号中。 除管道)  ( 字符外，其他所有有效的 Microsoft Excel 字符 (都可以在列名称中使用，包括空格。 必须将分隔的标识符用于 Microsoft Excel 列名，才能包括空格。 未指定的列名称将替换为驱动程序生成的名称，例如，第一列的 "Col1"。  
  
 在列名称中不能使用 ( # A0) 的管道字符，是否将该名称括在引号中。  
  
 使用文本驱动程序时，如果未指定列名，驱动程序将提供默认名称。 例如，驱动程序调用第一列 F1，第二列 F2，依此类推。
