---
title: "复制功能 |Microsoft 文档"
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
- duplicated functions [ODBC]
- compatibility [ODBC], duplicated functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], duplicated functions
- backward compatibility [ODBC], duplicated functions
ms.assetid: 641b16bc-f791-46d8-b093-31736473fe3d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b12ba1b5b8c70e6ab0f7efe6f0811984411a6022
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="duplicated-features"></a>重复的功能
以下的 ODBC 2。*x*由 ODBC 3 重复的函数。*x*函数。 因此，ODBC 2。*x*函数被弃用 ODBC 3 中。*x*。 ODBC 3。*x*函数称为替换函数。  
  
 当应用程序使用不推荐使用的 ODBC 2。*x*函数以及最基础的驱动程序是 ODBC 3。*x*驱动程序，驱动程序管理器映射到相应的替换函数的函数调用。 此规则的唯一例外是**SQLExtendedFetch**。 （请参阅下表的末尾脚注。）有关这些映射的详细信息，请参阅[映射弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)为了向后兼容的附录 g： 驱动程序准则中。  
  
 应用程序时使用替换函数以及基础的驱动程序是 ODBC 2。*x*驱动程序，驱动程序管理器映射到相应的不推荐使用函数的函数调用。  
  
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
  
 [1] 函数**SQLExtendedFetch**是重复这样的功能。**SQLFetchScroll**提供 ODBC 3 中相同的功能。*x*。 但是，驱动程序管理器未映射**SQLExtendedFetch**到**SQLFetchScroll**时针对 ODBC 3。*x*驱动程序。 有关详细信息，请参阅[驱动程序管理器的用途](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)为了向后兼容的附录 g： 驱动程序准则中。 驱动程序管理器映射**SQLFetchScroll**到**SQLExtendedFetch**时针对 ODBC 2。*x*驱动程序。  
  
> [!NOTE]  
>  该函数**SQLBindParam**是一种特殊情况。 **SQLBindParam**是重复的功能。 这不是 ODBC 2*.x*函数，但存在 Open Group 和 ISO 标准中的函数。 此函数提供的功能完全归入通过的**SQLBindParameter**。 因此，驱动程序管理器映射调用**SQLBindParam**到**SQLBindParameter**基础驱动程序时 ODBC 3。*x*驱动程序。 但是，当基础驱动程序是 ODBC 2*.x*驱动程序，驱动程序管理器不会执行此映射。
