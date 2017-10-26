---
title: "标头记录 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0e4b73bf94c2d90f34c1d06240cbcceb07702c7a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="header-record"></a>标头记录
标头记录中的字段包含有关函数的执行，包括返回代码，行计数、 状态记录数以及执行语句的类型的常规信息。 除非该函数将返回 SQL_INVALID_HANDLE，始终会创建标头记录。 标头记录中的字段的完整列表，请参阅[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函数说明。

