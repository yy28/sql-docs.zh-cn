---
title: 描述参数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f4d9284294707da0a469bf75ff9812ad5f7855bb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305938"
---
# <a name="describing-parameters"></a>描述参数
**SQLBind参数**具有描述参数的参数：其 SQL 类型、精度和缩放。 驱动程序使用此信息或*元数据*将参数值转换为数据源所需的类型。 乍一看，驱动程序似乎比应用程序更了解参数元数据;毕竟，驱动程序可以轻松地发现结果集列的元数据。 事实证明，情况并非如此。 首先，大多数数据源不为驱动程序提供发现参数元数据的方法。 其次，大多数应用程序已经知道元数据。  
  
 如果 SQL 语句在应用程序中是硬编码的，则应用程序编写器已经知道每个参数的类型。 如果 SQL 语句由应用程序在运行时构造，则应用程序可以在生成语句时确定元数据。 例如，当应用程序构造子句时  
  
```  
WHERE OrderID = ?  
```  
  
 它可以为 OrderID 列调用**SQLColumn。**  
  
 应用程序无法轻松确定参数元数据的唯一情况是用户输入参数化语句。 在这种情况下，应用程序调用**SQLPrepare**来准备语句 **，SQLNumParams**来确定参数数 **，SQLDescribeParam**来描述每个参数。 但是，如前所述，大多数数据源不为驱动程序提供发现参数元数据的方法，因此**SQLDescribeParam**并不得到广泛支持。
