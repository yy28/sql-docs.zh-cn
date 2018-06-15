---
title: 字符串函数 （Visual FoxPro ODBC 驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC string functions [ODBC]
- string functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], string functions
- FoxPro ODBC driver [ODBC], string functions
ms.assetid: 1974fd26-ef0d-45d5-860b-298917c8e9c3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1f89dabb9d46b29a4ec362cd012ff96de60c10e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904952"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>字符串函数 （Visual FoxPro ODBC 驱动程序）
下表列出了 Visual FoxPro ODBC 驱动程序; 支持 ODBC 字符串操作函数当相同的功能的 Visual FoxPro 语法不同于 ODBC 语法，将列等效 Visual FoxPro。  
  
|ODBC 语法|Visual FoxPro 语法|  
|------------------|---------------------------|  
|ASCII *(string_exp)*|ASC *(string_exp)*|  
|CHAR *（代码）*|CHR *(string_exp)*|  
|CONCAT *(string_exp1，string_exp2)*|*string_exp1 + string_exp2*|  
|差异 *(string_exp1，string_exp2)*||  
|插入 *(string_exp1，开始、 长度、 string_exp2)*|内容 *(string_exp1，开始、 长度、 string_exp2)*|  
|LCASE *(string_exp)*|较低 *(string_exp)*|  
|左 *(string_exp，计数)*||  
|长度 *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|重复 *(string_exp，计数)*|复制 *(string_exp，计数)*|  
|替换 *(string_exp1，string_exp2，string_exp3)*|STRTRAN *(string_exp1，string_exp2，string_exp3)*|  
|右 *(string_exp，计数)*||  
|RTRIM *(string_exp)*||  
|SOUNDEX *(string_exp)*||  
|空间 *（计数）*||  
|子字符串 *(string_exp，开始，长度)*|SUBSTR *(string_exp，开始，长度)*|  
|UCASE *(string_exp)*|上部 *(string_exp)*|
