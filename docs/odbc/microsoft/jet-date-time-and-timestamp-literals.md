---
title: Jet： 日期、 时间和时间戳文本 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 2325cd7e4a10e91f351aa2107c64c0978b843fa6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825835"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet：日期、时间和时间戳文本
最大互操作性，应用程序应传入使用 escape 子句语法的 ODBC 规范格式的日期文本：  
  
-   Date 文本的 {d '*值*'}，其中*valu*e 是在窗体"年-月-日"  
  
-   时间文字，{t '*值*'}，其中*valu*e 是在窗体"hh: mm:"  
  
 时间戳文本的 {ts*值*}，其中*valu*e 采用的形式"yyyy mm dd hh: mm: [.f...]"。
