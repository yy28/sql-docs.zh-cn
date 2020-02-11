---
title: 调用 SQLSetPos |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c64575777fc9210c36be5d417cd3def0c2c7102a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068677"
---
# <a name="calling-sqlsetpos"></a>调用 SQLSetPos
在 ODBC *2.x 中，* 指向行状态数组的指针是**SQLExtendedFetch**的参数。 行状态数组稍后通过调用**SQLSetPos**进行更新。 某些驱动程序依赖于此阵列在**SQLExtendedFetch**和**SQLSetPos**之间不会发生更改的情况。 在 ODBC 3.x 中，指向状态数组的指针是一个描述符*字段，因此*应用程序可以轻松地将其更改为指向不同的数组。 当 ODBC 1.x 应用程序正在*使用 odbc 2.x* *驱动程序，* 但调用**SQLSetStmtAttr**来设置数组状态指针并调用**SQLFetchScroll**来获取数据时，这可能是一个问题。 驱动程序管理器将它映射为对**SQLExtendedFetch**的调用序列。 在下面的代码中，当驱动程序管理器在*使用 ODBC 2.x*驱动程序时映射第二个**SQLSetStmtAttr**调用时，通常会引发错误：  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 如果在对**SQLExtendedFetch**的*调用之间没有*办法更改 ODBC 1.x 中的行状态指针，则会引发此错误。 相反，在使用 ODBC 2.x 驱动程序时，*驱动程序管理*器会执行以下步骤：  
  
1.  将内部驱动程序管理器标志*fSetPosError*初始化为 TRUE。  
  
2.  当应用程序调用**SQLFetchScroll**时，驱动程序管理器会将*FSETPOSERROR*设置为 FALSE。  
  
3.  当应用程序调用**SQLSetStmtAttr**设置 SQL_ATTR_ROW_STATUS_PTR 时，驱动程序管理器会将*fSetPosError*设置为等于设置为 true。  
  
4.  当应用程序调用**SQLSetPos**时，如果*fSetPosError*等于 TRUE，驱动程序管理器将引发 SQL_ERROR 与 SQLSTATE HY011 （现在不能设置特性）以指示应用程序在更改行状态指针之后但在调用**SQLSetPos**之前尝试调用**SQLFetchScroll** 。
