---
title: Jet：日期、时间和时间戳文本 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 372b7c1dab1ad8ff000fb88729c3b02e05d4a21c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299928"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet：日期、时间和时间戳文本
为了实现最大的互操作性，应用程序应使用转义子句语法来传递 ODBC 规范格式的日期文本：  
  
-   对于日期文本，为 {d '*value*'}，其中*valu*e 的格式为 "yyyy-mm-dd"  
  
-   对于时间文本，为 {t '*value*'}，其中*valu*e 的格式为 "hh： mm： ss"  
  
 对于 timestamp 文本 {ts '*value*'}，其中*valu*e 的格式为 "yyyy-mm-dd hh： mm： ss [. f ...]"。
