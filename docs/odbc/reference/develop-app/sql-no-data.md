---
title: SQL_NO_DATA |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a399a270eb1cd2f3daf9449c53b1f577a6b9545
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299787"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
ODBC 3 时*x*应用程序调用 ODBC 2 中的**SQLExecDirect**、 **SQLExecute**或**SQLParamData** 。*x*驱动程序执行搜索的 update 或 delete 语句，该语句不会影响数据源中的任何行，驱动程序应返回 SQL_SUCCESS，而不是 SQL_NO_DATA。 当使用 ODBC 2 时。*x*或 ODBC 3。使用 ODBC 3 的*x*应用程序。*x*驱动程序调用**SQLExecDirect**、 **SQLExecute**或**SQLParamData** ，其结果与 ODBC 3 相同。*x*驱动程序应返回 SQL_NO_DATA。
