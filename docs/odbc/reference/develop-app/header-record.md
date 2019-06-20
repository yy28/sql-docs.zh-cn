---
title: 标头记录 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7b6ffacb618dd2b7714be59814f3f1a88a52228
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208482"
---
# <a name="header-record"></a>标头记录
标头记录中的字段包含有关函数的执行，包括返回代码、 行计数、 状态记录数和执行的语句类型的一般信息。 除非该函数返回 SQL_INVALID_HANDLE 始终创建标头记录。 标头记录中的字段的完整列表，请参阅[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函数说明。
