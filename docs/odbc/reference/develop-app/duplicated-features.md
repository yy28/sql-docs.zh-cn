---
title: 重复的功能 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300477"
---
# <a name="duplicated-features"></a>重复的功能
以下 ODBC *2.x*函数已由 ODBC *3.x*函数复制。 因此，ODBC *2.x*函数在 ODBC *3.x*中被弃用。 ODBC *3.x*函数称为替换函数。  
  
 当应用程序使用弃用的 ODBC *2.x*函数，而基础驱动程序是 ODBC *3.x*驱动程序时，驱动程序管理器将函数调用映射到相应的替换函数。 此规则的唯一例外是**SQL 扩展获取**。 （请参阅下表末尾的脚注。有关这些映射的详细信息，请参阅附录 G：向后兼容性的驱动程序指南中[映射已弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)。  
  
 当应用程序使用替换函数，基础驱动程序是 ODBC *2.x*驱动程序时，驱动程序管理器将函数调用映射到相应的弃用函数。  
  
|ODBC *2.x*功能|ODBC *3.x*功能|  
|-------------------------|-------------------------|  
|**SQLAlloc连接**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLColattributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQL 扩展获取**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**， **SQLGetstmtAttr**|  
|**SQLSet 连接选项**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] 函数**SQL 扩展获取**是重复的功能;**SQLFetchScroll**在 ODBC *3.x*中提供了相同的功能。 但是，当与 ODBC *3.x*驱动程序发生对抗时，驱动程序管理器不会将**SQLAtoFetch**映射到**SQLFetchScroll。** 有关详细信息，请参阅[驱动程序管理器](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)在附录 G 中的"驱动程序管理器"中所做的"驱动程序指南"。 当与 ODBC *2.x*驱动程序发生对抗时，驱动程序管理器将**SQLFetchScroll**映射到**SQL 扩展获取**。  
  
> [!NOTE]
>  函数**SQLBindParam**是一个特例。 **SQLBindParam**是重复的功能。 这不是 ODBC *2.x*函数，而是开放组和 ISO 标准中存在的函数。 此函数提供的功能完全由**SQLBind参数**的功能包起来。 因此，当基础驱动程序是 ODBC *3.x*驱动程序时，驱动程序管理器将对**SQLBindParam**的调用映射到**SQLBind参数**。 但是，当基础驱动程序是 ODBC *2.x*驱动程序时，驱动程序管理器不执行此映射。
