---
title: 复制描述符 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d41cd744d39113c556c4ee8bc17411b7992e596
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002139"
---
# <a name="copying-descriptors"></a>复制描述符
调用**SQLCopyDesc**函数将一个描述符的字段复制到另一个描述符。 字段只能复制到应用程序描述符或 IPD，但不能复制到 IRD。 可以从任何类型的描述符复制字段。 仅复制为源和目标描述符定义的字段。 **SQLCopyDesc**不会复制 SQL_DESC_ALLOC_TYPE 字段，因为无法更改描述符的分配类型。 复制的字段覆盖现有字段。  
  
 一个语句句柄上的 ARD 可以用作另一个语句句柄上的 APD。 这允许应用程序在表之间复制行，而无需在应用程序级别复制数据。 为此，可在 INSERT 语句中以参数的参数描述符的形式重复使用行说明符来描述表的提取行。 要使此操作成功，SQL_MAX_CONCURRENT_ACTIVITIES 信息类型必须大于1。
