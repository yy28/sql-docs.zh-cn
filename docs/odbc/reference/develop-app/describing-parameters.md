---
title: 描述参数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bc752afc0cb5214e629a343c35464e612b57c36
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808965"
---
# <a name="describing-parameters"></a>描述参数
**SQLBindParameter**包含描述此参数的参数： 其 SQL 类型、 精度和小数位数。 驱动程序使用此信息，或*元数据，* 将参数值转换为所需的数据源的类型。 第一次看到它可能看起来驱动程序位于更有利于知道比应用程序; 的参数元数据毕竟，该驱动程序可以轻松地发现元数据，为结果集列。 事实证明，这不是这种情况。 首先，大多数数据源未提供的驱动程序来发现参数元数据的方法。 第二个，大多数应用程序已经知道元数据。  
  
 如果 SQL 语句是硬编码应用程序中，应用程序编写器已知道每个参数的类型。 如果应用程序在运行时构造 SQL 语句时，应用程序可以确定元数据生成该语句。 例如，当应用程序构造子句  
  
```  
WHERE OrderID = ?  
```  
  
 它可以调用**SQLColumns**订单 id 列。  
  
 应用程序无法轻松确定参数元数据的唯一情况是当用户输入的参数化的语句。 在这种情况下，应用程序调用**SQLPrepare**准备语句**SQLNumParams**来确定数目的参数，并**SQLDescribeParam**来描述每个参数。 但是，如前所述，大多数数据源不提供驱动程序来发现参数元数据，因此一种方法**SQLDescribeParam**并未得到广泛支持。
