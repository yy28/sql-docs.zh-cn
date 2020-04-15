---
title: 驱动程序管理器诊断示例 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 839095e5544cab73cdddd4f4b17a3d8d52136c9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305808"
---
# <a name="driver-manager-diagnostic-example"></a>驱动程序管理器诊断示例
驱动程序管理器还可以生成诊断消息。 例如，如果应用程序将无效的方向选项传递给**SQLDataSources，** 驱动程序管理器可能会格式化并从**SQLGetDiagRec 返回**以下值 ：  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 由于错误发生在驱动程序管理器中，因此它将前缀添加到其供应商 （[Microsoft]） 及其标识符 （[ODBC 驱动程序管理器]）的诊断消息中。
