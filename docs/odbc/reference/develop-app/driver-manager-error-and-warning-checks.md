---
title: "驱动程序管理器错误和警告检查 |Microsoft 文档"
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
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7d61068526b0f15b7de5ba58c09675f1d9b75e9e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="driver-manager-error-and-warning-checks"></a>驱动程序管理器错误和警告检查
驱动程序管理器完全或部分实现的许多功能，并因此检查所有或部分的错误和在这些函数中的警告。  
  
-   驱动程序管理器实现**SQLDataSources**和**SQLDrivers**和所有错误和警告在这些函数中的检查。  
  
-   驱动程序管理器检查是否驱动程序实现**SQLGetFunctions**。 如果该驱动程序不实现**SQLGetFunctions**，驱动程序管理器实现，并检查所有错误和警告在其中。  
  
-   驱动程序管理器部分实现**SQLAllocHandle**， **SQLConnect**， **SQLDriverConnect**， **SQLBrowseConnect**， **SQLFreeHandle**， **SQLGetDiagRec**，和**SQLGetDiagField**和在这些函数中出现某些错误检查。 它可能这些函数的某些返回作为该驱动程序相同的错误，因为同时执行类似操作。 例如，驱动程序管理器或驱动程序可能会返回 SQLSTATE IM008 （对话框中失败） 如果其中一个不能显示为一个登录对话框**SQLDriverConnect**。
