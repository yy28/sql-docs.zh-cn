---
title: 返回SQL_NO_DATA |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e2c806edd5d5647e09c00975ad7207ee5c2c876
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305108"
---
# <a name="returning-sql_no_data"></a>返回 SQL_NO_DATA
当使用 ODBC *3.x*驱动程序的 ODBC *2.x*应用程序调用**SQLExecDirect、SQLExecute**或**SQLParamData**，并且执行搜索的更新或删除语句，但不影响数据源上的任何行时，ODBC *3.x*驱动程序应返回SQL_SUCCESS。 **SQLExecute** 当使用 ODBC *3.x*驱动程序的应用程序调用*3.x* **SQLExecDirect、SQLExecute**或**SQLExecute** **SQLParamData**时具有相同的结果，ODBC *3.x*驱动程序应返回SQL_NO_DATA。  
  
 如果一批语句中搜索的更新或删除语句不会影响数据源中的任何行 **，SQLMore结果**将返回SQL_SUCCESS。 它不能返回SQL_NO_DATA，因为这意味着没有更多的结果，而不是从搜索的更新/删除的结果，没有影响行。
