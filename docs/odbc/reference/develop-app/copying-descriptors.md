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
manager: craigg
ms.openlocfilehash: da22ba86ea49532f460b081b13e18d6b7d95211c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042753"
---
# <a name="copying-descriptors"></a>复制描述符
**SQLCopyDesc**函数调用以将一个描述符字段复制到另一个描述符。 可以复制字段，仅对应用程序描述符或 IPD，而不是属于 IRD。 可以从任何类型的描述符复制字段。 复制源和目标描述符定义这些字段。 **SQLCopyDesc**不会复制 SQL_DESC_ALLOC_TYPE 字段，因为无法更改描述符的分配类型。 复制的字段会覆盖现有字段。  
  
 上一个语句句柄 ARD 可以充当另一个语句句柄上 APD。 这允许应用程序复制而不复制应用程序级别上的数据的表之间的行。 若要执行此操作，作为 INSERT 语句中的参数的参数描述符重用介绍提取的行的表的行描述符。 SQL_MAX_CONCURRENT_ACTIVITIES 信息类型必须是大于 1 的此操作才能成功。
