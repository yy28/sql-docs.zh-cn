---
description: 字符串函数（Visual FoxPro ODBC 驱动程序）
title: " (Visual FoxPro ODBC 驱动程序) 的字符串函数 |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC string functions [ODBC]
- string functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], string functions
- FoxPro ODBC driver [ODBC], string functions
ms.assetid: 1974fd26-ef0d-45d5-860b-298917c8e9c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ab2ecefb604183b0387a561f72494028c62d15f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471539"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>字符串函数（Visual FoxPro ODBC 驱动程序）
下表列出了 Visual FoxPro ODBC 驱动程序支持的 ODBC 字符串操作函数;当同一个函数的 Visual FoxPro 语法与 ODBC 语法不同时，将列出等效的 Visual FoxPro。  
  
|ODBC 语法|Visual FoxPro 语法|  
|------------------|---------------------------|  
|ASCII * (string_exp) *|ASC * (string_exp) *|  
|CHAR * (代码) *|CHR * (string_exp) *|  
|CONCAT * (string_exp1，string_exp2) *|*string_exp1 + string_exp2*|  
|差异 * (string_exp1，string_exp2) *||  
|插入 * (string_exp1，开始，长度，string_exp2) *|* (string_exp1、开始、长度 string_exp2*的内容) |  
|LCASE * (string_exp) *|降低 * (string_exp) *|  
|左 * (string_exp，计数) *||  
|* (STRING_EXP 长度) *|LEN * (string_exp) *|  
|LTRIM * (string_exp) *||  
|重复 * (string_exp，计数) *|复制 * (string_exp，计数) *|  
|替换 * (string_exp1，string_exp2 string_exp3) *|STRTRAN * (string_exp1，string_exp2 string_exp3) *|  
|RIGHT * (string_exp，计数) *||  
|RTRIM * (string_exp) *||  
|SOUNDEX * (string_exp) *||  
|空间 * (计数) *||  
|子字符串 * (string_exp，开始，长度) *|SUBSTR * (string_exp、start、length) *|  
|UCASE * (string_exp) *|* (string_exp) *|
