---
description: 描述参数
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a41bee40403cc3562c41ccc13a15c706a0772e27
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476749"
---
# <a name="describing-parameters"></a>描述参数
**SQLBindParameter** 具有描述参数的参数：其 SQL 类型、精度和小数位数。 驱动程序使用此信息或 *元数据* 将参数值转换为数据源所需的类型。 乍一看，驱动程序的位置可能与应用程序的参数元数据的位置更好;毕竟，驱动程序可以轻松发现结果集列的元数据。 事实证明，事实并非如此。 首先，大多数数据源不提供驱动程序发现参数元数据的方法。 其次，大多数应用程序已经知道了元数据。  
  
 如果在应用程序中硬编码 SQL 语句，则应用程序编写器已经知道每个参数的类型。 如果 SQL 语句是在运行时由应用程序构造的，则应用程序可以在生成语句时确定元数据。 例如，当应用程序构造子句时  
  
```  
WHERE OrderID = ?  
```  
  
 它可以为 "订单 Id" 列调用 **SQLColumns** 。  
  
 应用程序无法轻松确定参数元数据的唯一情况是用户输入参数化语句时。 在这种情况下，应用程序会调用 **SQLPrepare** 来准备语句， **SQLNumParams** 来确定参数的数目，并调用 **SQLDescribeParam** 来描述每个参数。 但是，如前所述，大多数数据源不提供驱动程序发现参数元数据的方法，因此 **SQLDescribeParam** 不受广泛支持。
