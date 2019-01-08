---
title: 重复的功能 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- duplicated functions [ODBC]
- compatibility [ODBC], duplicated functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], duplicated functions
- backward compatibility [ODBC], duplicated functions
ms.assetid: 641b16bc-f791-46d8-b093-31736473fe3d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84752b7e23c5394757764bf5ade57cb54004b01a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208306"
---
# <a name="duplicated-features"></a>重复的功能
以下 ODBC 2。*x* ODBC 3 个重复的函数。*x*函数。 因此，ODBC 2。*x*函数在 ODBC 3 中已弃用。*x*。 ODBC 3。*x*函数称为替换函数。  
  
 当应用程序使用不推荐使用的 ODBC 2。*x*函数并且基础驱动程序是 ODBC 3。*x*驱动程序，驱动程序管理器将映射到相应的替换函数的函数调用。 此规则的唯一例外是**SQLExtendedFetch**。 （请参阅下表末尾的脚注。）有关这些映射的详细信息，请参阅[映射已弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)中附录 g:为了向后兼容的驱动程序指南。  
  
 当应用程序使用替换函数和基础驱动程序是 ODBC 2。*x*驱动程序，驱动程序管理器将映射到相应的已弃用函数的函数调用。  
  
|ODBC 2。*x*函数|ODBC 3。*x*函数|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLExtendedFetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**， **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] 函数**SQLExtendedFetch**是重复的功能;**SQLFetchScroll**提供相同的功能在 ODBC 3。*x*。 但是，驱动程序管理器不映射**SQLExtendedFetch**到**SQLFetchScroll**时对 ODBC 3。*x*驱动程序。 有关详细信息，请参阅[驱动程序管理器的用途](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)中附录 g:为了向后兼容的驱动程序指南。 驱动程序管理器映射**SQLFetchScroll**到**SQLExtendedFetch**时对 ODBC 2。*x*驱动程序。  
  
> [!NOTE]
>  该函数**SQLBindParam**是一种特殊情况。 **SQLBindParam**是重复的功能。 这不是 ODBC 2 *.x*函数，但存在 Open Group 和 ISO 标准中的函数。 此函数提供的功能完全包含的**SQLBindParameter**。 因此，驱动程序管理器将映射到调用**SQLBindParam**到**SQLBindParameter**基础驱动程序时 ODBC 3。*x*驱动程序。 但是，当基础驱动程序是 ODBC 2 *.x*驱动程序，驱动程序管理器不会执行此映射。
