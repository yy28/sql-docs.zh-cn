---
title: SQLBindParam 映射 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26f9bdc0564b98132bb5ec413c99917e78e4d62e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855175"
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 映射
**SQLBindParam**无法真正调用不推荐使用因为它的存在永远不会在 ODBC 中; 但是，它仍表示重复的功能 — 驱动程序管理器需要将其导出，因为 ISO 和打开组兼容的应用程序将使用它。 因为**SQLBindParameter**包含的所有功能**SQLBindParam**， **SQLBindParam**将被映射的**SQLBindParameter**(当基础驱动程序是 ODBC 3 *.x*驱动程序)。 ODBC 3 *.x*驱动程序不需要实现**SQLBindParam**。  
  
## <a name="remarks"></a>备注  
 当以下调用到**SQLBindParam**进行：  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 驱动程序管理器调用**SQLBindParameter**在驱动程序中，如下所示：  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 请参阅[ODBC 64-Bit 信息](../../../odbc/reference/odbc-64-bit-information.md)，如果你的应用程序将在 64 位操作系统上运行。  
  
## <a name="see-also"></a>请参阅  
 [映射已弃用的函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
