---
title: SQLGetTypeInfo （文本文件驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetTypeInfo
ms.assetid: 05a58975-093c-4bd9-bd72-b5f0026a6e36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c1c38b66e9b8a3c1cbed4a3712f7af866935089
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63210225"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo（文本文件驱动程序）
> [!NOTE]  
>  本主题提供了文本文件驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 在生成的表中返回的类型 (TYPE_NAME) 名称**SQLGetTypeInfo**将是最常用的数据源的名称。  
  
 SQL_ALL_EXCEPT_LIKE 将返回在可搜索的列中的字节，计数器、 Double、 单、 长时间和 Short 数据类型。 （LIKE 功能可以通过将值转换为使用 ODBC 规范转换函数，然后执行比较的字符。）  
  
 使用文本驱动程序时， **SQLGetTypeInfo**返回 CASE_SENSITIVE 值为 FALSE 的文本数据类型 （CHAR 和 LONGCHAR） 时的数据类型实际上是区分大小写。
