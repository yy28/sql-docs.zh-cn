---
title: 数据类型支持 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b5fe4081d0786ace40dd027606a830982798075e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044956"
---
# <a name="data-type-support"></a>数据类型支持
ODBC 驱动程序必须支持至少一个 SQL_CHAR 和 SQL_VARCHAR。 支持的其他数据类型取决于驱动程序或数据源的 SQL-92 的一致性级别。 应用程序应调用**SQLGetTypeInfo**以确定驱动程序支持的数据类型。  
  
 有关数据类型的详细信息，请参阅[附录 d:数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。
