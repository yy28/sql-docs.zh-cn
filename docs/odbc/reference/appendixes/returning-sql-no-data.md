---
title: "返回 SQL_NO_DATA |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf27a50915d9af31eaa280525736cacf7faf06db
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="returning-sqlnodata"></a>返回 SQL_NO_DATA
当一个 ODBC 2。*x*应用程序但 ODBC 3*.x*驱动程序调用**SQLExecDirect**， **SQLExecute**，或**SQLParamData**，和搜索的更新或删除语句已执行，但未影响任何行在数据源，ODBC 3*.x*驱动程序应返回 SQL_SUCCESS。 当 ODBC 3*.x*应用程序使用 ODBC 3*.x*驱动程序调用**SQLExecDirect**， **SQLExecute**，或**SQLParamData**与相同的结果，ODBC 3*.x*驱动程序应返回 SQL_NO_DATA。  
  
 如果搜索的更新或删除语句中的一批语句不会影响数据源中的任何行**SQLMoreResults**返回 SQL_SUCCESS。 它不能返回 SQL_NO_DATA，因为这可能意味着有更多结果，不是有搜索更新/删除影响任何行从一个结果。
