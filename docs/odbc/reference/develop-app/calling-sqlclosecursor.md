---
title: 调用 SQLCloseCursor |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2feab58de28e39747a1d9c819f9f15426b156151
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306270"
---
# <a name="calling-sqlclosecursor"></a>调用 SQLCloseCursor
由于**SQLCloseCursor**与**SQLFreeStmt**与具有SQL_CLOSE几乎相同，因此驱动程序管理器不会映射此函数。 可映射替换函数，以便现有的 ODBC *2.x*应用程序可以使用新功能轻松移动到 ODBC *3.x。* 通过这样的移动，此类应用程序可以更轻松地开始以模块化方式在条件代码内部使用新的 ODBC *3.x*功能。 **SQLCloseCursor**不表示任何新功能。 应用程序通过使用SQL_CLOSE从**SQLFreeStmt**移动到**SQLCloseCursor**不会获得任何优势。
