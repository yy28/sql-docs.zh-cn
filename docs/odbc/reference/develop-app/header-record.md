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
ms.openlocfilehash: 7f5fe5cf6aae0d5953cc82b845396dd4164c7fa3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139017"
---
# <a name="header-record"></a>标头记录
标头记录中的字段包含有关函数执行的一般信息，包括返回代码、行计数、状态记录数和所执行的语句类型。 始终会创建标头记录，除非该函数返回 SQL_INVALID_HANDLE。 有关标头记录中字段的完整列表，请参阅[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函数说明。
