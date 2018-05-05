---
title: Dbms 中的事务支持 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 7095120f0a41bb4df5a3607c55abeb3a9da194f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="transaction-support-in-dbmss"></a>Dbms 中的事务支持
某些数据库，如 dBASE、 Paradox 和 Btrieve，尤其是桌面数据库不支持事务。 即使在支持事务的数据库，之间没有在类型的 SQL 语句可以是在事务中的变体。 有关详细信息，请参阅中的 SQL_TXN_CAPABLE 选项[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。
