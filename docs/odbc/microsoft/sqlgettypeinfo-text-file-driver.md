---
description: SQLGetTypeInfo（文本文件驱动程序）
title: SQLGetTypeInfo (文本文件驱动程序) |Microsoft Docs
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
ms.openlocfilehash: 1c023c4b18cd335f562541ad10885546f2163d10
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449159"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo（文本文件驱动程序）
> [!NOTE]  
>  本主题提供特定于文本文件驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 由 **SQLGetTypeInfo** 生成的表中返回的类型 (TYPE_NAME) 的名称将是数据源最常使用的名称。  
  
 对于 Byte、Counter、Double、Single、Long 和 Short 数据类型，将在可搜索列中返回 SQL_ALL_EXCEPT_LIKE。  (可以通过使用 ODBC 规范转换函数将值转换为字符，然后执行比较来实现类似功能。 )   
  
 使用文本驱动程序时，当数据类型确实区分大小写时， **SQLGetTypeInfo** 将为文本数据类型返回 CASE_SENSITIVE 值为 FALSE (CHAR 和 LONGCHAR) 。
