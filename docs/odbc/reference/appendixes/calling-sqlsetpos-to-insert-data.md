---
title: "调用以插入数据的 SQLSetPos |Microsoft 文档"
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
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e9d768ea5c16b199dc316726cb425b75d409bf1f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="calling-sqlsetpos-to-insert-data"></a>调用 SQLSetPos 以插入数据
当一个 ODBC 2。*x*应用程序使用 ODBC 3*.x*驱动程序调用**SQLSetPos**与*操作*SQL_ADD，驱动程序管理器的自变量未映射到此调用**SQLBulkOperations**。 如果 ODBC 3*.x*驱动程序应使用的应用程序调用**SQLSetPos** SQL_ADD，驱动程序应支持该操作。  
  
 行为的一个主要区别时**SQLSetPos**使用调用就是处于状态 S6 时发生 SQL_ADD。 在 ODBC 2。*x*，驱动程序返回 S1010 时**SQLSetPos**调用时使用中状态 S6 SQL_ADD (光标具有定位与后**SQLFetch**)。 ODBC 3 中*.x*， **SQLBulkOperations**与*操作*的 SQL_ADD 可以调用状态 S6 中。 行为的另一个主要区别在于**SQLBulkOperations**与*操作*的 SQL_ADD 可以是在状态 S5 中调用，而**SQLSetPos**与**操作**的 SQL_ADD 不能。 对于 ODBC 3 中相同的调用可以发生的语句转换，*.x*，请参阅[附录 b: ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
