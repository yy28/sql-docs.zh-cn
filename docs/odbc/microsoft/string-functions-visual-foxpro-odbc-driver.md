---
title: 字符串函数（Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
ms.openlocfilehash: db1fbaffbee0f74625f4a11cad3b961f194e3829
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948779"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>字符串函数（Visual FoxPro ODBC 驱动程序）
下表列出了 Visual FoxPro ODBC 驱动程序支持的 ODBC 字符串操作函数;当同一个函数的 Visual FoxPro 语法与 ODBC 语法不同时，将列出等效的 Visual FoxPro。  
  
|ODBC 语法|Visual FoxPro 语法|  
|------------------|---------------------------|  
|ASCII *（string_exp）*|ASC *（string_exp）*|  
|CHAR *（代码）*|CHR *（string_exp）*|  
|CONCAT *（string_exp1、string_exp2）*|*string_exp1 + string_exp2*|  
|差异 *（string_exp1、string_exp2）*||  
|INSERT *（string_exp1、start、length、string_exp2）*|内容 *（string_exp1、开始、长度、string_exp2）*|  
|LCASE *（string_exp）*|LOWER *（string_exp）*|  
|LEFT *（string_exp，count）*||  
|长度 *（string_exp）*|LEN *（string_exp）*|  
|LTRIM *（string_exp）*||  
|重复 *（string_exp，count）*|复制 *（string_exp、计数）*|  
|REPLACE *（string_exp1、string_exp2、string_exp3）*|STRTRAN *（string_exp1、string_exp2、string_exp3）*|  
|RIGHT *（string_exp，count）*||  
|RTRIM *（string_exp）*||  
|SOUNDEX *（string_exp）*||  
|空间 *（计数）*||  
|SUBSTRING *（string_exp、start、length）*|SUBSTR *（string_exp、start、length）*|  
|UCASE *（string_exp）*|上部 *（string_exp）*|
