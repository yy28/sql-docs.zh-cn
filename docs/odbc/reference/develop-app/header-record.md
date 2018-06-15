---
title: 标头记录 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 095135d0fb199ddcc89203d5ba5cc4cbf334d273
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908952"
---
# <a name="header-record"></a>标头记录
标头记录中的字段包含有关函数的执行，包括返回代码，行计数、 状态记录数以及执行语句的类型的常规信息。 除非该函数将返回 SQL_INVALID_HANDLE，始终会创建标头记录。 标头记录中的字段的完整列表，请参阅[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函数说明。
