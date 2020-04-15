---
title: SQLGetTypeInfo（文本文件驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294997"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo（文本文件驱动程序）
> [!NOTE]  
>  本主题提供特定于文本文件驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLGetTypeInfo**生成的表中返回的类型（TYPE_NAME）的名称将是数据源最常用的名称。  
  
 SQL_ALL_EXCEPT_LIKE将在字节、计数器、双、单、长和短数据类型的 SEARCHABLE 列中返回。 （可以通过使用 ODBC 规范转换函数将值转换为字符，然后执行比较来实现 LIKE 功能。  
  
 使用文本驱动程序时 **，SQLGetTypeInfo**会为文本数据类型（CHAR 和 LONGCHAR）返回 FALSE 的CASE_SENSITIVE值，当数据类型实际上区分大小写时。
