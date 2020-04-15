---
title: 调用 SQLSetPos 以插入数据 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb374b2506d55b400207c8f60bdf42bb6bb4065e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306598"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>调用 SQLSetPos 以插入数据
当使用 ODBC *3.x*驱动程序的 ODBC *2.x*应用程序调用**SQLSetPos**时，*操作*参数为 SQL_ADD，驱动程序管理器不会将此调用映射到**SQLBulk 操作**。 如果 ODBC *3.x*驱动程序应使用使用 SQL_ADD 调用**SQLSetPos**的应用程序，则驱动程序应支持该操作。  
  
 当使用 SQL_ADD调用**SQLSetPos**时，行为上会出现一个主要差异，当在状态 S6 中调用 SQLSetPos 时。 在 ODBC *2.x*中，当 SQLSetPos 在状态 S6 中调用 SQL_ADD **sqlSetPos**时（在游标已使用**SQLFetch**定位后），驱动程序返回 S1010。 在 ODBC *3.x*中，可在状态 S6 中调用操作*SQL_ADD的***SQLBulk 操作**。 行为的第二个主要区别是，具有SQL_ADD*操作*的**SQLBulk 操作**可以在状态 S5 中调用，而操作**SQL_ADD的****SQLSetPos**不能调用。 有关 ODBC *3.x*中同一调用可能发生的语句转换，请参阅[附录 B：ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
