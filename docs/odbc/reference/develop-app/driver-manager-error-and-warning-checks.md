---
title: "驱动程序管理器错误和警告检查 |Microsoft 文档"
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
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce87b9dbed8cfa6ca621cb72c36220c13ecb0929
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager-error-and-warning-checks"></a>驱动程序管理器错误和警告检查
驱动程序管理器完全或部分实现的许多功能，并因此检查所有或部分的错误和在这些函数中的警告。  
  
-   驱动程序管理器实现**SQLDataSources**和**SQLDrivers**和所有错误和警告在这些函数中的检查。  
  
-   驱动程序管理器检查是否驱动程序实现**SQLGetFunctions**。 如果该驱动程序不实现**SQLGetFunctions**，驱动程序管理器实现，并检查所有错误和警告在其中。  
  
-   驱动程序管理器部分实现**SQLAllocHandle**， **SQLConnect**， **SQLDriverConnect**， **SQLBrowseConnect**， **SQLFreeHandle**， **SQLGetDiagRec**，和**SQLGetDiagField**和在这些函数中出现某些错误检查。 它可能这些函数的某些返回作为该驱动程序相同的错误，因为同时执行类似操作。 例如，驱动程序管理器或驱动程序可能会返回 SQLSTATE IM008 （对话框中失败） 如果其中一个不能显示为一个登录对话框**SQLDriverConnect**。
