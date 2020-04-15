---
title: 数据类型支持 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abfe85ee32fb9ff4a8499c9949c0685563fec70
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284424"
---
# <a name="data-type-support"></a>数据类型支持
ODBC 驱动程序必须至少支持一个SQL_CHAR和SQL_VARCHAR。 对其他数据类型的支持由驱动程序或数据源的 SQL-92 一致性级别决定。 应用程序应调用**SQLGetTypeInfo**以确定驱动程序支持的数据类型。  
  
 有关数据类型的详细信息，请参阅[附录 D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。
