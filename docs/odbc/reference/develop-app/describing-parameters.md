---
title: 描述参数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 629241f2385eeb3059800d35288b9c71d1d0ac97
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="describing-parameters"></a>描述参数
**SQLBindParameter**包含描述参数的自变量： 其 SQL 类型、 精度和小数位数。 驱动程序使用此信息，或*元数据，*将参数值转换为所需的数据源的类型。 从表面看，这看起来可能驱动程序处于更有利知道比应用程序; 的参数元数据的位置毕竟，该驱动程序可以轻松地发现元数据的一个结果集列。 事实证明，这不是这种情况。 首先，大多数数据源不提供驱动程序来发现参数元数据的方法。 第二个，大多数应用程序已经知道元数据。  
  
 如果 SQL 语句是硬编码在应用程序中，应用程序编写器已知道每个参数的类型。 如果应用程序在运行时构造 SQL 语句时，应用程序可以为生成语句确定的元数据。 例如，当应用程序构造子句  
  
```  
WHERE OrderID = ?  
```  
  
 它可以调用**SQLColumns**为 orderid 列。  
  
 应用程序无法轻松确定参数元数据的唯一情况是当用户输入的参数化的语句。 在这种情况下，在应用程序调用**SQLPrepare**准备语句， **SQLNumParams**以确定多个参数，和**SQLDescribeParam**来描述每个参数。 但是，如前所述，大多数数据源不提供了驱动程序来发现参数元数据，因此**SQLDescribeParam**不受广泛支持。
