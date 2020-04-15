---
title: SQL_NO_DATA |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299787"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
当一个ODBC 3。*x*应用程序在 ODBC 2 中调用**SQLExecDirect、SQLExecute**或**SQLExecute****SQLParamData。***x*驱动程序执行不影响数据源上任何行的搜索更新或删除语句，驱动程序应返回SQL_SUCCESS，而不是SQL_NO_DATA。 当一个ODBC 2。*x*或 ODBC 3。*x*使用 ODBC 3 的应用程序。*x*驱动程序调用**SQLExecDirect、SQLExecute**或**SQLExecute****SQLParamData，** 其结果相同，即 ODBC 3。*x*驱动程序应返回SQL_NO_DATA。
