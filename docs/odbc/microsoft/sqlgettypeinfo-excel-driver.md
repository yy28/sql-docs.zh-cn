---
description: SQLGetTypeInfo（Excel 驱动程序）
title: SQLGetTypeInfo (Excel 驱动程序) |Microsoft Docs
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
ms.openlocfilehash: ca7e70d9f26a87ededb21bc6c48f3d3cd31d8af3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339953"
---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo（Excel 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 Excel 驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 由 **SQLGetTypeInfo** 生成的表中返回的类型 (TYPE_NAME) 的名称将是数据源最常使用的名称。  
  
 对于 Byte、Counter、Double、Single、Long 和 Short 数据类型，将在可搜索列中返回 SQL_ALL_EXCEPT_LIKE。  (可以通过使用 ODBC 规范转换函数将值转换为字符，然后执行比较来实现类似功能。 )   
  
 使用 Microsoft Excel 驱动程序时，ODBC 类型名称将在 **SQLGetTypeInfo**返回的 TYPE_NAME 列中返回。
