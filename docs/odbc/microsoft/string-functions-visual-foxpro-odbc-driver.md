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
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854825"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>字符串函数（Visual FoxPro ODBC 驱动程序）
下表列出了支持的 Visual FoxPro ODBC 驱动程序; ODBC 字符串操作函数在相同的功能的 Visual FoxPro 语法与 ODBC 语法不同，会列出等效 Visual FoxPro。  
  
|ODBC 语法|Visual FoxPro 语法|  
|------------------|---------------------------|  
|ASCII *(string_exp)*|ASC *(string_exp)*|  
|CHAR *（代码）*|CHR *(string_exp)*|  
|CONCAT *(string_exp1，string_exp2)*|*string_exp1 + string_exp2*|  
|差异 *(string_exp1，string_exp2)*||  
|插入 *(string_exp1，开始、 长度、 string_exp2)*|内容 *(string_exp1，开始、 长度、 string_exp2)*|  
|LCASE *(string_exp)*|较低 *(string_exp)*|  
|左侧 *(string_exp，计数)*||  
|长度 *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|重复 *(string_exp，计数)*|复制 *(string_exp，计数)*|  
|替换为 *(string_exp1，string_exp2，string_exp3)*|STRTRAN *(string_exp1，string_exp2，string_exp3)*|  
|右 *(string_exp，计数)*||  
|RTRIM *(string_exp)*||  
|SOUNDEX *(string_exp)*||  
|空间 *（计数）*||  
|子字符串 *(string_exp，开始，长度)*|SUBSTR *(string_exp，开始，长度)*|  
|UCASE *(string_exp)*|上部 *(string_exp)*|
