---
title: SQLGetTypeInfo (dBASE Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetTypeInfo
ms.assetid: 6e9ce02b-97c7-4c1a-91e0-829df7459c84
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90bfbe29fd011f8b62527854f0ca5a179d8f63cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224531"
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供 dBASE 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 在生成的表中返回的类型 (TYPE_NAME) 名称**SQLGetTypeInfo**将是最常用的数据源的名称。  
  
 SQL_ALL_EXCEPT_LIKE 将返回在可搜索的列中的字节，计数器、 Double、 单、 长时间和 Short 数据类型。 （LIKE 功能可以通过将值转换为使用 ODBC 规范转换函数，然后执行比较的字符。）
