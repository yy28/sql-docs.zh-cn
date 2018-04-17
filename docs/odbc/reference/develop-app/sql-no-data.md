---
title: SQL_NO_DATA |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 48e50a556f5d1caa05170772d95a702d436d1722
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlnodata"></a>SQL_NO_DATA
当一个 ODBC 3。*x*应用程序调用**SQLExecDirect**， **SQLExecute**，或**SQLParamData** ODBC 2 中。*x*驱动程序以执行搜索的更新或删除不会影响数据源，该驱动程序中的任何行的语句应返回 SQL_SUCCESS，不 SQL_NO_DATA。 当一个 ODBC 2。*x*或 ODBC 3。*x*应用程序使用 ODBC 3。*x*驱动程序调用**SQLExecDirect**， **SQLExecute**，或**SQLParamData**与相同的结果，ODBC 3。*x*驱动程序应返回 SQL_NO_DATA。
