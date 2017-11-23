---
title: "描述符转换 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- state transitions [ODBC], descriptor
- transitioning states [ODBC], descriptor
- descriptor transitions [ODBC]
ms.assetid: 0cf24fe6-5e3c-45fa-81b8-4f52ddf8501d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 82dd5d9fe22a33c50ac33426f71a25524a2b5c2f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="descriptor-transitions"></a>描述符转换
ODBC 描述符具有以下三种状态。  
  
|State|Description|  
|-----------|-----------------|  
|D0|未分配的描述符|  
|D1i|隐式分配的描述符|  
|D1e|显式分配的描述符|  
  
 下表显示每个 ODBC 函数如何影响描述符状态。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> 未分配|D1i<br /><br /> 隐式|D1e<br /><br /> 显式|  
|------------------------|----------------------|----------------------|  
|D1i [1]|--|--|  
|D1e [2]|--|--|  
  
 [1] 该行显示转换时*HandleType*已 SQL_HANDLE_STMT。  
  
 [2] 该行显示转换时*HandleType*已 SQL_HANDLE_DESC。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> 未分配|D1i<br /><br /> 隐式|D1e<br /><br /> 显式|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> 未分配|D1i<br /><br /> 隐式|D1e<br /><br /> 显式|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|(IH)[2]|(HY017)|D0|  
  
 [1] 该行显示转换时*HandleType*已 SQL_HANDLE_STMT。  
  
 [2] 该行显示转换时*HandleType*已 SQL_HANDLE_DESC。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 和 SQLGetDescRec  
  
|D0<br /><br /> 未分配|D1i<br /><br /> 隐式|D1e<br /><br /> 显式|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 和 SQLSetDescRec  
  
|D0<br /><br /> 未分配|D1i<br /><br /> 隐式|D1e<br /><br /> 显式|  
|------------------------|----------------------|----------------------|  
|(IH)[1]|--|--|  
  
 [1] 该行显示转换时*DescriptorHandle*已 ARD、 APD，或 IPD，句柄或 (对于**SQLSetDescField**) 时*DescriptorHandle*已 IRD 的句柄和*FieldIdentifier* SQL_DESC_ARRAY_STATUS_PTR 或 SQL_DESC_ROWS_PROCESSED_PTR。  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 函数  
  
|D0<br /><br /> 未分配|D1i<br /><br /> 隐式|D1e<br /><br /> 显式|  
|------------------------|----------------------|----------------------|  
|--|--|--|
