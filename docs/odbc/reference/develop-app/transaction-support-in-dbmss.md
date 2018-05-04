---
title: Dbms 中的事务支持 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0acd20649609d6899edbd4146799d9c002da1c6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="transaction-support-in-dbmss"></a>Dbms 中的事务支持
某些数据库，如 dBASE、 Paradox 和 Btrieve，尤其是桌面数据库不支持事务。 即使在支持事务的数据库，之间没有在类型的 SQL 语句可以是在事务中的变体。 有关详细信息，请参阅中的 SQL_TXN_CAPABLE 选项[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。
