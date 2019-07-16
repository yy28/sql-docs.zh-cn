---
title: SQL_NO_DATA | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f899e7a034e1ec5fc967d834caad3a4ccc4caa1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041831"
---
# <a name="sqlnodata"></a>SQL_NO_DATA
当 ODBC 3。*x*应用程序调用**SQLExecDirect**， **SQLExecute**，或者**SQLParamData** ODBC 2 中。*x*驱动程序以执行搜索的 update 或 delete 语句，但不影响任何行在数据源，该驱动程序应返回 SQL_SUCCESS，不 sql_no_data 为止。 当 ODBC 2。*x*或 ODBC 3。*x*应用程序使用 ODBC 3。*x*驱动程序调用**SQLExecDirect**， **SQLExecute**，或**SQLParamData**使用相同的结果，ODBC 3。*x*驱动程序应返回 sql_no_data 为止。
