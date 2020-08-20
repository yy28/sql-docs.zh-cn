---
description: DBMS 中的事务支持
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8e0b3433e0f666af100cce5e72e36b685533b1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487450"
---
# <a name="transaction-support-in-dbmss"></a>DBMS 中的事务支持
某些数据库（特别是 dBASE、Paradox 和 Btrieve 等桌面数据库）不支持事务。 甚至在支持事务的数据库中，事务中的 SQL 语句类型都有不同的变化。 有关详细信息，请参阅 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函数说明中的 SQL_TXN_CAPABLE 选项。
