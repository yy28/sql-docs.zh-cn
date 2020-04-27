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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b70b58e4760959db102450b5f8b7beed042df95
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "81294997"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo（文本文件驱动程序）
> [!NOTE]  
>  本主题提供特定于文本文件驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 **SQLGetTypeInfo**生成的表中返回的类型（TYPE_NAME）的名称将是数据源最常使用的名称。  
  
 对于 Byte、Counter、Double、Single、Long 和 Short 数据类型，将在可搜索列中返回 SQL_ALL_EXCEPT_LIKE。 （可通过使用 ODBC 规范转换函数将值转换为字符，然后执行比较来实现类似的功能。）  
  
 使用文本驱动程序时，如果数据类型确实区分大小写，则**SQLGetTypeInfo**将返回文本数据类型（CHAR 和 LONGCHAR）的 CASE_SENSITIVE 值 FALSE。
