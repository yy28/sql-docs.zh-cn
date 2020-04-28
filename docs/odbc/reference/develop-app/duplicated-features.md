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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 00f5529cfbfacebcad78a0a4433e84f34034694a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300477"
---
# <a name="duplicated-features"></a>重复的功能
以下 ODBC 2.x*函数已被 odbc* *1.x 函数重复*。 因此 *，odbc 2.x 函数在*odbc 2.x 中已*弃用。* ODBC 1.x 函数称为*替换函数。*  
  
 当应用程序使用已弃用的 ODBC *2.x 函数，* 并且基础驱动程序是 odbc 1.x*驱动程序*时，驱动程序管理器会将函数调用映射到相应的替换函数。 此规则的唯一例外是**SQLExtendedFetch**。 （请参见下表末尾的脚注。）有关这些映射的详细信息，请参阅附录 G：驱动程序准则中的[映射弃用的函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)，以实现向后兼容性。  
  
 当应用程序使用替代函数，而基础*驱动程序是 ODBC 2.x*驱动程序时，驱动程序管理器会将函数调用映射到相应的不推荐使用的函数。  
  
|ODBC *2.x*函数|ODBC *2.x*函数|  
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
|**SQLParamOptions**|**SQLSetStmtAttr**、 **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] 函数**SQLExtendedFetch**是重复的功能;**SQLFetchScroll** *在 ODBC 1.x*中提供了相同的功能。 但是，在 SQLExtendedFetch *ODBC 1.x*驱动程序时，驱动程序管理器不会将**SQLExtendedFetch**映射到**SQLFetchScroll** 。 有关详细信息，请参阅附录 G：用于向后兼容的驱动程序准则中[的驱动程序管理器的](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)作用。 当*使用 ODBC 2.x*驱动程序时，驱动程序管理器会将**SQLFetchScroll**映射到**SQLExtendedFetch** 。  
  
> [!NOTE]
>  函数**SQLBindParam**是一种特殊情况。 **SQLBindParam**是重复功能。 这不是 ODBC 2.x 函数，而是开放组和 ISO 标准中存在*的函数。* 此函数提供的功能完全由**SQLBindParameter**的归入。 因此，当基础*驱动程序为 ODBC 3.x*驱动程序时，驱动程序管理器会将对**SQLBindParam**的调用映射到**SQLBindParameter** 。 但是，当基础*驱动程序是 ODBC 2.x*驱动程序时，驱动程序管理器不会执行此映射。
