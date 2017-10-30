---
title: "SQLBindParam 映射 |Microsoft 文档"
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
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d94cdc4b73bd176ae7af002ab290b795ad87d39e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 映射
**SQLBindParam**无法真正调用不推荐使用因为它已存在永远不会 ODBC 中; 但是，它仍表示重复的功能-驱动程序管理器需要将其导出，因为 ISO 和打开组 – 符合应用程序将使用它。 因为**SQLBindParameter**包含的所有功能**SQLBindParam**， **SQLBindParam**将映射的顶部**SQLBindParameter**(基础驱动程序时 ODBC 3*.x*驱动程序)。 ODBC 3*.x*驱动程序不需要实现**SQLBindParam**。  
  
## <a name="remarks"></a>注释  
 当以下调用到**SQLBindParam**进行：  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 驱动程序管理器调用**SQLBindParameter** ，如下所示驱动程序中：  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)，如果你的应用程序将在 64 位操作系统上运行。  
  
## <a name="see-also"></a>另请参阅  
 [映射函数弃用](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)

