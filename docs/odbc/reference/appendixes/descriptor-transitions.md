---
title: 描述符转换 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC], descriptor
- transitioning states [ODBC], descriptor
- descriptor transitions [ODBC]
ms.assetid: 0cf24fe6-5e3c-45fa-81b8-4f52ddf8501d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec5c26bdde8a0d470f2d93e753504bf1c51edcc0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307038"
---
# <a name="descriptor-transitions"></a>描述符转换
ODBC 描述符具有以下三种状态。  
  
|State|说明|  
|-----------|-----------------|  
|D0|未分配的描述符|  
|D1i|隐式分配的描述符|  
|D1e|显式分配的描述符|  
  
 下表显示了每个 ODBC 函数如何影响描述符状态。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> 未分配|D1i<br /><br /> 隐式|D1e<br /><br /> 显式|  
|------------------------|----------------------|----------------------|  
|D1i [1]|--|--|  
|D1e [2]|--|--|  
  
 [1] 此行显示 SQL_HANDLE_STMT *HandleType*时的转换。  
  
 [2] 在 SQL_HANDLE_DESC *HandleType*时，该行显示转换。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> 未分配|D1i<br /><br /> 隐式|D1e<br /><br /> 显式|  
|------------------------|----------------------|----------------------|  
|IH|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> 未分配|D1i<br /><br /> 隐式|D1e<br /><br /> 显式|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|IHpps-2|(HY017)|D0|  
  
 [1] 此行显示 SQL_HANDLE_STMT *HandleType*时的转换。  
  
 [2] 在 SQL_HANDLE_DESC *HandleType*时，该行显示转换。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 和 SQLGetDescRec  
  
|D0<br /><br /> 未分配|D1i<br /><br /> 隐式|D1e<br /><br /> 显式|  
|------------------------|----------------------|----------------------|  
|IH|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 和 SQLSetDescRec  
  
|D0<br /><br /> 未分配|D1i<br /><br /> 隐式|D1e<br /><br /> 显式|  
|------------------------|----------------------|----------------------|  
|IH2|--|--|  
  
 [1] 此行显示当*DescriptorHandle*是 ARD、APD 或 IPD 的句柄时，或者（对于**SQLSetDescField**）， *DescriptorHandle*是 IRD 的句柄 *，而 FieldIdentifier*是 SQL_DESC_ARRAY_STATUS_PTR 或 SQL_DESC_ROWS_PROCESSED_PTR 的。  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 函数  
  
|D0<br /><br /> 未分配|D1i<br /><br /> 隐式|D1e<br /><br /> 显式|  
|------------------------|----------------------|----------------------|  
|--|--|--|
