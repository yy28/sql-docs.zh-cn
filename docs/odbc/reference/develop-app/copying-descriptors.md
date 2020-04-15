---
title: 复制描述符 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e2e5897afc3673a21396e256df04d25008c8cdf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301666"
---
# <a name="copying-descriptors"></a>复制描述符
调用**SQLCopyDesc**函数将一个描述符的字段复制到另一个描述符。 字段只能复制到应用程序描述符或 IPD，但不能复制到 IRD。 可以从任何类型的描述符复制字段。 仅复制为源和目标描述符定义的字段。 **SQLCopyDesc**不会复制SQL_DESC_ALLOC_TYPE字段，因为无法更改描述符的分配类型。 复制的字段覆盖现有字段。  
  
 一个语句句柄上的 ARD 可以充当另一个语句句柄上的 APD。 这允许应用程序在表之间复制行，而无需在应用程序级别复制数据。 为此，描述表的提取行的行描述符将重新用作 INSERT 语句中参数的参数描述符。 SQL_MAX_CONCURRENT_ACTIVITIES信息类型必须大于 1 才能成功此操作。
