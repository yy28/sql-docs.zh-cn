---
title: "驱动程序管理器诊断示例 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3f373fe012c2b791329fea35ca853021e70274eb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager-diagnostic-example"></a>驱动程序管理器诊断示例
驱动程序管理器还可以生成诊断消息。 例如，如果应用程序传递的方向无效选项**SQLDataSources**，驱动程序管理器可能格式和返回中的以下值**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 在驱动程序管理器中出错，因为它添加前缀到诊断消息其供应商 ([Microsoft]) 以及其标识符 （[ODBC 驱动程序管理器]）。
