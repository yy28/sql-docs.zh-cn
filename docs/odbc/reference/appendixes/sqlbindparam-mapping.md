---
title: SQLBindParam 映射 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1df595722297c91dc75398470912188e109e278
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305437"
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 映射
**SQLBindParam**不能真正称为弃用，因为它在 ODBC 中从未存在过;但是，它仍然表示重复的功能 - 驱动程序管理器需要导出它，因为 ISO 和符合开放组的应用程序将使用它。 由于**SQLBind参数**包含**SQLBindParam**的所有功能，因此**SQLBindParam**将映射到**SQLBind 参数**之上（当基础驱动程序是 ODBC *3.x*驱动程序时）。 ODBC *3.x*驱动程序不需要实现**SQLBindParam**。  
  
## <a name="remarks"></a>备注  
 当对**SQLBindParam**进行以下调用时：  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 驱动程序管理器在驱动程序中调用**SQLBind参数**，如下所示：  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 如果应用程序将在 64 位操作系统上运行，请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>另请参阅  
 [映射已弃用的函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
