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
manager: craigg
ms.openlocfilehash: c9a3d63f0bf1923905c5281655aff2af294b8284
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241328"
---
# <a name="data-type-support"></a>数据类型支持
ODBC 驱动程序必须支持至少一个 SQL_CHAR 和 SQL_VARCHAR。 支持的其他数据类型取决于驱动程序或数据源的 SQL-92 的一致性级别。 应用程序应调用**SQLGetTypeInfo**以确定驱动程序支持的数据类型。  
  
 有关数据类型的详细信息，请参阅[附录 d:数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。
