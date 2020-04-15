---
title: 调用 SQLSetPos |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], calling
- upgrading applications [ODBC], SQLSetPos
- backward compatibility [ODBC], SqlSetPos
- application upgrades [ODBC], SQLSetPos
ms.assetid: 846354b8-966c-4c2c-b32f-b0c8e649cedd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46cfbb4e2e6b60f620cd7e38272bf9308ece91bc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306238"
---
# <a name="calling-sqlsetpos"></a>调用 SQLSetPos
在 ODBC *2.x*中，指向行状态数组的指针是**SQL 扩展获取的**参数。 行状态数组后来被调用**SQLSetPos**更新。 某些驱动程序依赖于此数组在**SQL 扩展获取**和**SQLSetPos**之间不更改这一事实。 在 ODBC *3.x*中，指向状态数组的指针是一个描述符字段，因此应用程序可以轻松地将其更改为指向其他数组。 当 ODBC *3.x*应用程序使用 ODBC *2.x*驱动程序，但正在调用**SQLSetStmtAttr**来设置阵列状态指针并调用**SQLFetchScroll**来获取数据时，这可能是一个问题。 驱动程序管理器将其映射为对**SQL 扩展获取**的调用序列。 在以下代码中，当驱动程序管理器映射第二个**SQLSetStmtAttr**调用时，使用 ODBC *2.x*驱动程序时，通常会引发错误：  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 如果无法在调用**SQLExtendedFetch**之间更改 ODBC *2.x*中的行状态指针，则将引发该错误。 相反，驱动程序管理器在使用 ODBC *2.x*驱动程序时执行以下步骤：  
  
1.  初始化内部驱动程序管理器标志*fSetPosError*到 TRUE。  
  
2.  当应用程序调用**SQLFetchScroll**时，驱动程序管理器将*fSetPosError*设置为 FALSE。  
  
3.  当应用程序调用**SQLSetStmtAttr**设置为SQL_ATTR_ROW_STATUS_PTR时，驱动程序管理器将*fSetPosError*设置为等于 TRUE。  
  
4.  当应用程序调用**SQLSetPos**时 *，fSetPosError*等于 TRUE 时，驱动程序管理器会使用 SQLSTATE HY011（现在无法设置属性）引发SQL_ERROR，以指示应用程序在更改行状态指针后但在调用**SQLFetch**之前尝试调用**SQLSetPos。**
