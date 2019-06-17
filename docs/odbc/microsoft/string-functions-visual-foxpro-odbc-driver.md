---
title: 字符串函数 （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a9e1c94eec150cc24522cd6e4c57eb35b4a2126
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270919"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>字符串函数（Visual FoxPro ODBC 驱动程序）
下表列出了支持的 Visual FoxPro ODBC 驱动程序; ODBC 字符串操作函数在相同的功能的 Visual FoxPro 语法与 ODBC 语法不同，会列出等效 Visual FoxPro。  
  
|ODBC 语法|Visual FoxPro 语法|  
|------------------|---------------------------|  
|ASCII *(string_exp)*|ASC *(string_exp)*|  
|CHAR *(code)*|CHR *(string_exp)*|  
|CONCAT *(string_exp1, string_exp2)*|*string_exp1 + string_exp2*|  
|DIFFERENCE *(string_exp1, string_exp2)*||  
|插入 *(string_exp1，开始、 长度、 string_exp2)*|内容 *(string_exp1，开始、 长度、 string_exp2)*|  
|LCASE *(string_exp)*|LOWER *(string_exp)*|  
|LEFT *(string_exp, count)*||  
|LENGTH *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|REPEAT *(string_exp, count)*|REPLICATE *(string_exp, count)*|  
|REPLACE *(string_exp1, string_exp2, string_exp3)*|STRTRAN *(string_exp1, string_exp2, string_exp3)*|  
|右 *(string_exp，计数)*||  
|RTRIM *(string_exp)*||  
|SOUNDEX *(string_exp)*||  
|空间 *（计数）*||  
|子字符串 *(string_exp，开始，长度)*|SUBSTR *(string_exp，开始，长度)*|  
|UCASE *(string_exp)*|UPPER *(string_exp)*|
