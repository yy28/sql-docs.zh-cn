---
title: 调用 SQLSetPos 以插入数据 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c7424206318436532cad62690b01427f079a589
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159277"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>调用 SQLSetPos 以插入数据
当 ODBC 2。*x*应用程序使用 ODBC 3 *.x*驱动程序调用**SQLSetPos**与*操作*SQL_ADD，驱动程序管理器的自变量不映射到此调用**SQLBulkOperations**。 如果 ODBC 3 *.x*驱动程序应使用调用的应用程序**SQLSetPos** SQL_ADD，使用该驱动程序应支持该操作。  
  
 在行为中的一个主要区别时**SQLSetPos**使用调用 SQL_ADD 发生状态 S6 中调用时。 在 ODBC 2。*x*，该驱动程序返回 S1010 时**SQLSetPos**调用时使用处于状态 S6 SQL_ADD (光标定位使用完后**SQLFetch**)。 在 ODBC 3 *.x*， **SQLBulkOperations**与*操作*SQL_ADD 的可调用状态 S6 中。 在行为中的另一个主要区别在于**SQLBulkOperations**与*操作*可以是 SQL_ADD 状态 S5 中调用，而**SQLSetPos**与**操作**SQL_ADD 的不能。 语句转换可能会出现的相同的调用在 ODBC 3 *.x*，请参阅[附录 b:状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
