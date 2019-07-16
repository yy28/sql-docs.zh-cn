---
title: 驱动程序管理器错误和警告检查 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d0b136b9748de1991888abb0c19bc0d2ac65ea0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046967"
---
# <a name="driver-manager-error-and-warning-checks"></a>驱动程序管理器错误和警告检查
驱动程序管理器完全或部分实现的许多功能，并因此检查所有或部分的错误和警告在这些函数中。  
  
-   驱动程序管理器实现**SQLDataSources**并**SQLDrivers** ，并检查所有错误和警告在这些函数中。  
  
-   驱动程序管理器检查驱动程序是否实现**SQLGetFunctions**。 如果该驱动程序不实现**SQLGetFunctions**，驱动程序管理器实现，并检查所有错误和警告中它。  
  
-   驱动程序管理器部分实现**SQLAllocHandle**， **SQLConnect**， **SQLDriverConnect**， **SQLBrowseConnect**， **SQLFreeHandle**， **SQLGetDiagRec**，和**SQLGetDiagField**并在这些函数中的某些错误检查。 因为同时执行类似的操作，它可能返回的某些函数作为驱动程序相同的错误。 例如，驱动程序管理器或驱动程序可能会返回 SQLSTATE IM008 （失败的对话框） 如果其中一个是无法显示为一个登录对话框**SQLDriverConnect**。
