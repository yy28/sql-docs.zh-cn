---
title: SQL_ARD_TYPE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 683b81f82094aa33deef86ffc19dc8c5c0a53a27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270437"
---
# <a name="sqlardtype"></a>SQL_ARD_TYPE
SQL_ARD_TYPE 类型标识符用于指示在缓冲区中的数据将 ARD SQL_DESC_CONCISE_TYPE 字段中指定的类型。 中输入 SQL_ARD_TYPE *TargetType*是对的调用的参数**SQLGetData**而不是特定的数据类型和允许的应用程序更改的数据缓冲区的类型通过更改描述符字段。 此值将绑定的数据类型 *\*TargetValuePtr*缓冲区描述符字段。 (对的调用中未输入 SQL_ARD_TYPE **SQLBindCol**或**SQLBindParameter**因为绑定的缓冲区的类型已绑定到的 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 字段，并可以更改任何时候通过更改这些字段之一。）  
  
 SQL_ARD_TYPE 类型标识符可用于指定前导精度和秒的精度的时间间隔数据类型的非默认值和类型的精度和小数位数 SQL_C_NUMERIC 数据值。 有关详细信息，请参阅[重写默认前导和秒间隔数据类型的精度](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)并[重写默认精度和小数位数数值数据类型](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)、 本附录中更高版本。
