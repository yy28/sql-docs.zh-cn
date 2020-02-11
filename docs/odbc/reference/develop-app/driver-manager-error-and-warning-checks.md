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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046967"
---
# <a name="driver-manager-error-and-warning-checks"></a>驱动程序管理器错误和警告检查
驱动程序管理器完全或部分实现多个函数，因此检查这些函数中的所有错误和警告。  
  
-   驱动程序管理器实现**SQLDataSources**和**SQLDrivers** ，并检查这些函数中的所有错误和警告。  
  
-   驱动程序管理器将检查驱动程序是否实现了**SQLGetFunctions**。 如果驱动程序未实现**SQLGetFunctions**，则驱动程序管理器将实现并检查其中的所有错误和警告。  
  
-   驱动程序管理器部分实现**SQLAllocHandle**、 **SQLConnect**、 **SQLDriverConnect**、 **SQLBrowseConnect**、 **SQLFreeHandle**、 **SQLGetDiagRec**和**SQLGetDiagField** ，并检查这些函数中的一些错误。 由于这两个函数都执行类似的操作，因此它可能会返回与此类函数的驱动程序相同的错误。 例如，如果两个 IM008 不能为**SQLDriverConnect**显示登录对话框，驱动程序管理器或驱动程序可能返回 SQLSTATE （对话框失败）。
