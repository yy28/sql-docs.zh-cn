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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e2e5897afc3673a21396e256df04d25008c8cdf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301666"
---
# <a name="copying-descriptors"></a>复制描述符
调用**SQLCopyDesc**函数将一个描述符的字段复制到另一个描述符。 字段只能复制到应用程序描述符或 IPD，但不能复制到 IRD。 可以从任何类型的描述符复制字段。 仅复制为源和目标描述符定义的字段。 **SQLCopyDesc**不会复制 SQL_DESC_ALLOC_TYPE 字段，因为无法更改描述符的分配类型。 复制的字段覆盖现有字段。  
  
 一个语句句柄上的 ARD 可以用作另一个语句句柄上的 APD。 这允许应用程序在表之间复制行，而无需在应用程序级别复制数据。 为此，可在 INSERT 语句中以参数的参数描述符的形式重复使用行说明符来描述表的提取行。 要使此操作成功，SQL_MAX_CONCURRENT_ACTIVITIES 信息类型必须大于1。
