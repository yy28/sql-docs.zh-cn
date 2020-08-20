---
description: 调用 SQLCloseCursor
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 925617d79266f0b50ef9b38586b31af91311b63e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494767"
---
# <a name="calling-sqlclosecursor"></a>调用 SQLCloseCursor
由于 **SQLCloseCursor** 与具有 SQL_CLOSE 的 **SQLFreeStmt** 几乎相同，因此，驱动程序管理器不会映射该函数。 将映射替换函数，以便*现有的 odbc* *2.x 应用程序*可以通过使用新函数轻松移动到 ODBC 2.x。 此类移动使此类应用程序可以更轻松地以模块化方式在条件代码内开始使用新*的 ODBC 2.x 功能。* **SQLCloseCursor** 不表示任何新功能。 应用程序不能通过使用 SQL_CLOSE 从**SQLFreeStmt**移到**SQLCloseCursor**获得任何优势。
