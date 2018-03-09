---
title: "调用 SQLSetPos |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], calling
- upgrading applications [ODBC], SQLSetPos
- backward compatibility [ODBC], SqlSetPos
- application upgrades [ODBC], SQLSetPos
ms.assetid: 846354b8-966c-4c2c-b32f-b0c8e649cedd
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 70351e468a6038a26b7b647d6bc7c64d3263f3d6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="calling-sqlsetpos"></a>调用 SQLSetPos
在 ODBC 2。*x*，指向行状态数组的指针时的自变量**SQLExtendedFetch**。 行状态数组更高版本已更新通过调用**SQLSetPos**。 某些驱动程序具有依赖于此数组不会更改之间的事实**SQLExtendedFetch**和**SQLSetPos**。 在 ODBC 3。*x*、 指向状态数组的指针是一个描述符字段，因此应用程序可以轻松地将其更改为指向另一个数组。 这可能会造成问题时 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序调用，但**SQLSetStmtAttr**设置数组状态指针和正在调用**SQLFetchScroll**提取数据。 驱动程序管理器将其映射为对的调用序列**SQLExtendedFetch**。 在下面的代码中，将通常会引发错误时驱动程序管理器映射第二个**SQLSetStmtAttr**在使用 ODBC 2 时调用*.x*驱动程序：  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 无法更改 ODBC 2 中的行状态指针时，将引发错误。*x*之间调用**SQLExtendedFetch**。 相反，驱动程序管理器执行以下步骤使用 ODBC 2 时*.x*驱动程序：  
  
1.  初始化内部的驱动程序管理器标志*fSetPosError*为 TRUE。  
  
2.  在应用程序调用**SQLFetchScroll**，驱动程序管理器设置*fSetPosError*为 FALSE。  
  
3.  在应用程序调用**SQLSetStmtAttr**若要设置 SQL_ATTR_ROW_STATUS_PTR，驱动程序管理器设置*fSetPosError*相等设置为 True。  
  
4.  在应用程序调用**SQLSetPos**，与*fSetPosError*等于 TRUE，驱动程序管理器引发与 SQLSTATE HY011 SQL_ERROR （不能设置属性现在），则指示应用程序尝试调用**SQLSetPos**之后更改行状态指针，但在调用之前**SQLFetchScroll**。
