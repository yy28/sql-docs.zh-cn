---
title: Calling SQLSetPos | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 70d574f867934af87ac7b5071b7f30bc9e89bccf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199444"
---
# <a name="calling-sqlsetpos"></a>调用 SQLSetPos
在 ODBC 2。*x*，指向行状态数组的指针时的参数**SQLExtendedFetch**。 行状态数组更高版本已更新通过调用**SQLSetPos**。 某些驱动程序已依赖于此数组不会更改之间的事实**SQLExtendedFetch**并**SQLSetPos**。 在 ODBC 3。*x*、 状态数组的指针是描述符字段，因此应用程序可以轻松地将其更改为指向另一个数组。 这会在 ODBC 3 时出现问题。*x*应用程序使用 ODBC 2。*x*驱动程序但在调用**SQLSetStmtAttr**设置数组状态指针时调用**SQLFetchScroll**来提取数据。 驱动程序管理器将其映射为一系列调用**SQLExtendedFetch**。 在下面的代码中，将通常情况下引发错误时驱动程序管理器映射第二个**SQLSetStmtAttr**使用 ODBC 2 时调用 *.x*驱动程序：  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 如果没有办法更改行状态指针 ODBC 2 中的，将引发错误。*x*调用之间**SQLExtendedFetch**。 相反，驱动程序管理器执行以下步骤时使用的 ODBC 2 *.x*驱动程序：  
  
1.  初始化内部的驱动程序管理器标志*fSetPosError*为 TRUE。  
  
2.  当应用程序调用**SQLFetchScroll**，驱动程序管理器设置*fSetPosError*为 FALSE。  
  
3.  当应用程序调用**SQLSetStmtAttr**若要设置 SQL_ATTR_ROW_STATUS_PTR，驱动程序管理器设置*fSetPosError*等于为 True。  
  
4.  当应用程序调用**SQLSetPos**，使用*fSetPosError*等于 TRUE，驱动程序管理器将引发具有 SQLSTATE HY011 SQL_ERROR （属性不能立即设置） 以指示应用程序已尝试调用**SQLSetPos**后更改行状态指针，但在调用之前**SQLFetchScroll**。
