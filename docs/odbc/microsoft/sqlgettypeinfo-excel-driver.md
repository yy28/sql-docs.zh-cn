---
title: SQLGetTypeInfo（Excel 驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Excel Driver
- Excel driver [ODBC], SQLGetTypeInfo
ms.assetid: 708845be-e6a1-4677-8113-c52819a43fa4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64befe30be9ed7988e0c9348e9335eb632dd975c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295067"
---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo（Excel 驱动程序）
> [!NOTE]  
>  本主题提供特定于 Excel 驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLGetTypeInfo**生成的表中返回的类型（TYPE_NAME）的名称将是数据源最常用的名称。  
  
 SQL_ALL_EXCEPT_LIKE将在字节、计数器、双、单、长和短数据类型的 SEARCHABLE 列中返回。 （可以通过使用 ODBC 规范转换函数将值转换为字符，然后执行比较来实现 LIKE 功能。  
  
 使用 Microsoft Excel 驱动程序时，ODBC 类型名称将返回**在 SQLGetTypeInfo**返回的TYPE_NAME列中。
