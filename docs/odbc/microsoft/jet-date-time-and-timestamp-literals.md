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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bb7f0fb02049b6d2f1897c4f495035aee2858f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085494"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet：日期、时间和时间戳文本
为了实现最大的互操作性，应用程序应使用转义子句语法来传递 ODBC 规范格式的日期文本：  
  
-   对于日期文本，为 {d '*value*'}，其中*valu*e 的格式为 "yyyy-mm-dd"  
  
-   对于时间文本，为 {t '*value*'}，其中*valu*e 的格式为 "hh： mm： ss"  
  
 对于 timestamp 文本 {ts '*value*'}，其中*valu*e 的格式为 "yyyy-mm-dd hh： mm： ss [. f ...]"。
