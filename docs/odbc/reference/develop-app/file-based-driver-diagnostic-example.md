---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: decb09098cee4b9ab6473e3c622b9917a89e9b09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061525"
---
# <a name="file-based-driver-diagnostic-example"></a>基于文件的驱动程序诊断示例
基于文件的驱动程序充当 ODBC 驱动程序和数据源同时。 在 ODBC 连接并作为数据源，它会因此生成错误和警告都作为一个组件。 因为它也是接口与驱动程序管理器的组件，其格式，并返回参数**SQLGetDiagRec**。  
  
 例如，如果 dBASE Microsoft® 驱动程序无法分配足够的内存，它可能会返回以下值从**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 因为此错误与数据源无关时，该驱动程序仅添加前缀到诊断消息供应商 ([Microsoft]) 和驱动程序 ([ODBC dBASE 驱动程序])。  
  
 如果该驱动程序找不到文件 Employee.dbf，它可能会返回以下值从**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 到数据源与此错误，因为该驱动程序会添加的文件格式的数据源 ([dBASE]) 作为前缀到诊断消息中。 因为该驱动程序也是对接与数据源的组件，它为供应商 ([Microsoft]) 和驱动程序 ([ODBC dBASE 驱动程序]) 添加前缀。
