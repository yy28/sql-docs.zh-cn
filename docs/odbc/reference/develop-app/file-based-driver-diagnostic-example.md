---
title: 基于文件的驱动程序诊断示例 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f09e4f4758b6276836b08f02b24fb31dd1fadc7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305635"
---
# <a name="file-based-driver-diagnostic-example"></a>基于文件的驱动程序诊断示例
基于文件的驱动程序既充当 ODBC 驱动程序，又充当数据源。 因此，它可以生成错误和警告，同时作为 ODBC 连接中的组件和数据源生成。 因为它也是与驱动程序管理器接口的组件，因此它格式化并返回**SQLGetDiagRec**的参数。  
  
 例如，如果 dBASE 的 Microsoft ®驱动程序无法分配足够的内存，它可能会从**SQLGetDiarec**返回以下值 ：  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 由于此错误与数据源无关，驱动程序仅向供应商 （[Microsoft]） 和驱动程序（[ODBC dBASE 驱动程序]）的诊断消息添加了前缀。  
  
 如果驱动程序找不到文件 Employ.dbf，它可能会从**SQLGetDiagRec**返回以下值 ：  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 由于此错误与数据源相关，驱动程序添加了数据源 （[dBASE]） 的文件格式作为诊断消息的前缀。 由于驱动程序也是与数据源接口的组件，因此添加了供应商（[微软]）和驱动程序（[ODBC dBASE 驱动程序]）的前缀。
