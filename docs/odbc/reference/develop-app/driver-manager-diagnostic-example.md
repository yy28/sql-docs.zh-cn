---
title: 驱动程序管理器诊断示例 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b8a63fc35dbedc1074f8fe713e8a87b207dad6c3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="driver-manager-diagnostic-example"></a>驱动程序管理器诊断示例
驱动程序管理器还可以生成诊断消息。 例如，如果应用程序传递的方向无效选项**SQLDataSources**，驱动程序管理器可能格式和返回中的以下值**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 在驱动程序管理器中出错，因为它添加前缀到诊断消息其供应商 ([Microsoft]) 以及其标识符 （[ODBC 驱动程序管理器]）。
