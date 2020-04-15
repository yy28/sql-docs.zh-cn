---
title: SQL_ARD_TYPE |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7e28d6babb7db8364697ae62092256396b44914
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305028"
---
# <a name="sql_ard_type"></a>SQL_ARD_TYPE
SQL_ARD_TYPE类型标识符用于指示缓冲区中的数据将属于 ARD SQL_DESC_CONCISE_TYPE 字段中指定的类型。 SQL_ARD_TYPE在调用**SQLGetData**而不是特定数据类型的*TargetType*参数中输入，并使应用程序能够通过更改描述符字段来更改缓冲区的数据类型。 此值将*\*TargetValuePtr*缓冲区的数据类型与描述符字段进行关系。 （SQL_ARD_TYPE不会在调用**SQLBindCol**或**SQLBind参数**时输入，因为绑定缓冲区的类型已绑定到SQL_DESC_TYPE和SQL_DESC_CONCISE_TYPE字段，并且可以随时通过更改这些字段中的任何一个进行更改。  
  
 SQL_ARD_TYPE类型标识符可用于为间隔数据类型的前导精度和秒精度指定非默认值，以及SQL_C_NUMERIC数据类型的精度和缩放值。 有关详细信息，请参阅本附录后面的[间隔数据类型](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)和[超值默认精度和"数字数据类型的覆盖默认精度"和"覆盖默认精度"和](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)"覆盖"精度。
