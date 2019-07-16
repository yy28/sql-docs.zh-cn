---
title: Dbms 中的事务支持 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72353e9917996ecacdc5971b4a11f9c73718ba43
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037629"
---
# <a name="transaction-support-in-dbmss"></a>DBMS 中的事务支持
某些数据库，如 dBASE、 Paradox 和 Btrieve，尤其是桌面数据库不支持事务。 支持事务的数据库，甚至之间是中的 SQL 语句类型可以是在事务中的变体。 有关详细信息，请参阅中的 SQL_TXN_CAPABLE 选项[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。
