---
title: 调用 SQLCloseCursor |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da5a674f86228c71a26e621936dc711a688a684d
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793945"
---
# <a name="calling-sqlclosecursor"></a>调用 SQLCloseCursor
因为**SQLCloseCursor**几乎与相同**SQLFreeStmt** SQL_CLOSE，与驱动程序管理器未映射此函数。 替换函数映射，以便现有 ODBC *2.x*应用程序可以轻松地将移动到 ODBC *3.x* ，使用的新功能。 这种移动简化此类应用程序，若要开始使用新的 ODBC *3.x*以模块化方式的条件代码内的功能。 **SQLCloseCursor**不表示任何新功能。 应用程序不会通过将移到获得任何优势**SQLCloseCursor**从**SQLFreeStmt**与 SQL_CLOSE。
