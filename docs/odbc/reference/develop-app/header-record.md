---
description: 标头记录
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4de764381e54a0b3485130c1a3bdf25b2a9bf9fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476639"
---
# <a name="header-record"></a>标头记录
标头记录中的字段包含有关函数执行的一般信息，包括返回代码、行计数、状态记录数和所执行的语句类型。 始终会创建标头记录，除非该函数返回 SQL_INVALID_HANDLE。 有关标头记录中字段的完整列表，请参阅 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 函数说明。
