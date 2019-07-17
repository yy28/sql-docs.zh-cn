---
title: Jet：日期、 时间和时间戳文本 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085494"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet：日期、时间和时间戳文本
最大互操作性，应用程序应传入使用 escape 子句语法的 ODBC 规范格式的日期文本：  
  
-   Date 文本的 {d '*值*'}，其中*valu*e 是在窗体"年-月-日"  
  
-   时间文字，{t '*值*'}，其中*valu*e 是在窗体"hh: mm:"  
  
 时间戳文本的 {ts*值*}，其中*valu*e 采用的形式"yyyy mm dd hh: mm: [.f...]"。
