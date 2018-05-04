---
title: Jet： 日期、 时间和时间戳文本 |Microsoft 文档
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
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc36c46885a358e1ca453901fd72362ed1dbb32b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet： 日期、 时间和时间戳文本
最大互操作性，应用程序应传递中使用 escape 子句语法的 ODBC 规范格式的日期文本：  
  
-   Date 文本的 {d '*值*}，其中*valu*e 采用格式"yyyy-月-日"  
  
-   时间文字，{t '*值*}，其中*valu*e 采用格式"hh: mm:"  
  
 时间戳文本的 {ts*值*}，其中*valu*e 采用的形式"yyyy mm dd hh: mm: [.f...]"。
