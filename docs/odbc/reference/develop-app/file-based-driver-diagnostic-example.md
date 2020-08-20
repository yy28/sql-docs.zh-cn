---
description: 基于文件的驱动程序诊断示例
title: 基于文件的驱动程序诊断示例 |Microsoft Docs
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
ms.openlocfilehash: 8986ebaa8c4ecf0ac18f4e043eb731df35054884
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499857"
---
# <a name="file-based-driver-diagnostic-example"></a>基于文件的驱动程序诊断示例
基于文件的驱动程序作为 ODBC 驱动程序和数据源。 因此，它可以在 ODBC 连接和数据源中同时生成错误和警告。 由于它也是与驱动程序管理器进行交互的组件，因此它将格式化并返回 **SQLGetDiagRec**的参数。  
  
 例如，如果 Microsoft® driver for dBASE 未能分配足够的内存，则它可能从 **SQLGetDiagRec**返回以下值：  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 由于此错误与数据源无关，因此驱动程序只为供应商 ( [Microsoft] ) 和驱动程序 ( [ODBC dBASE Driver] ) 中的诊断消息添加了前缀。  
  
 如果驱动程序找不到文件 node.js，则它可能从 **SQLGetDiagRec**返回以下值：  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 由于此错误与数据源相关，因此驱动程序添加了数据源的文件格式 ( [dBASE] ) 作为诊断消息的前缀。 由于驱动程序也是与数据源接口的组件，因此它为供应商 ( [Microsoft] ) 和驱动程序 ( [ODBC dBASE Driver] ) 添加了前缀。
