---
title: "复制描述符 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8cd2ea29713d3bf1e05e76de21397f71dd30c824
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="copying-descriptors"></a>复制描述符
**SQLCopyDesc**函数调用以将一个描述符字段复制到另一个描述符。 仅对应用程序描述符或 IPD，但不是属于 IRD，可以复制字段。 可以从任何类型的描述符复制字段。 仅在源和目标描述符定义这些字段会复制。 **SQLCopyDesc**不会复制 SQL_DESC_ALLOC_TYPE 字段中，因为不能更改描述符的分配类型。 复制的字段覆盖现有的字段。  
  
 一条语句句柄上的 ARD 可以充当另一个语句句柄上 APD。 这允许应用程序将行而不复制应用程序级别的数据的表之间复制。 若要执行此操作，描述读取的行的表的行描述符将作为重复使用 INSERT 语句中的参数的参数描述符。 SQL_MAX_CONCURRENT_ACTIVITIES 信息类型必须是大于 1 即可成功执行此操作。

