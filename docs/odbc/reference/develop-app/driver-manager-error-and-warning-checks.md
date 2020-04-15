---
title: 驱动程序管理器错误和警告检查 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee8a0f5ebfac8b6f87281806f07989f4980eb9b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305778"
---
# <a name="driver-manager-error-and-warning-checks"></a>驱动程序管理器错误和警告检查
驱动程序管理器全部或部分实现许多功能，因此检查这些函数中的所有或某些错误和警告。  
  
-   驱动程序管理器实现**SQLDataSources**和**SQLDriver，** 并检查这些函数中的所有错误和警告。  
  
-   驱动程序管理器检查驱动程序是否实现**SQLGet 函数**。 如果驱动程序未实现**SQLGet 功能**，驱动程序管理器将实现并检查其中的所有错误和警告。  
  
-   驱动程序管理器部分实现**SQLAllocHandle、** **SQLConnect**、 **SQLDriverConnect、** **SQLBrowseConnect、** **SQLFreeHandle、** **SQLGetDiagRec**和**SQLGetDiagField，** 并检查这些函数中的一些错误。 对于其中一些函数，它可能会返回与驱动程序相同的错误，因为两者都执行类似的操作。 例如，如果任一驱动程序无法显示**SQLDriverConnect**的登录对话框，则驱动程序管理器或驱动程序可能会返回 SQLSTATE IM008（对话框失败）。
