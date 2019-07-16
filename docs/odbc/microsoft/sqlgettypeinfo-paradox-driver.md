---
title: SQLGetTypeInfo （Paradox 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLGetTypeInfo
ms.assetid: e65063c7-ba9e-4cf0-ac13-4bb5bd2937db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c212584972f4a7e329d124cc8512be3b1f7a6b9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898617"
---
# <a name="sqlgettypeinfo-paradox-driver"></a>SQLGetTypeInfo（Paradox 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 Paradox 驱动程序的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 在生成的表中返回的类型 (TYPE_NAME) 名称**SQLGetTypeInfo**将是最常用的数据源的名称。  
  
 SQL_ALL_EXCEPT_LIKE 将返回在可搜索的列中的字节，计数器、 Double、 单、 长时间和 Short 数据类型。 (可通过将值转换为字符使用 ODBC 规范转换函数，实现类似功能，然后执行比较。)
