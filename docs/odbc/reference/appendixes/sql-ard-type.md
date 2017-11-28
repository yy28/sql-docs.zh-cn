---
title: "SQL_ARD_TYPE |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1c789c560adbb01d4c9c0bd2700dd3d1b0757f04
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlardtype"></a>SQL_ARD_TYPE
SQL_ARD_TYPE 类型标识符用于指示缓冲区中的数据将在 ARD SQL_DESC_CONCISE_TYPE 字段中指定的类型。 在中输入 SQL_ARD_TYPE *TargetType*对的调用的自变量**SQLGetData**而不是特定的数据类型和允许应用程序更改的数据类型的缓冲区通过更改描述符字段。 此值相关联的数据类型 *\*TargetValuePtr*描述符字段的缓冲区。 (对的调用中未输入 SQL_ARD_TYPE **SQLBindCol**或**SQLBindParameter**因为绑定缓冲区的类型已绑定到 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 字段，并可以更改任何时候通过更改这些字段之一。）  
  
 SQL_ARD_TYPE 类型标识符可以用于指定前导精度和秒精度的 interval 数据类型的非默认值和类型的精度和小数位数 SQL_C_NUMERIC 数据值。 有关详细信息，请参阅[重写默认前导空格和 Interval 数据类型的秒精度](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)和[重写默认精度和小数位数数值数据类型](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)、 本附录内容更高版本。
