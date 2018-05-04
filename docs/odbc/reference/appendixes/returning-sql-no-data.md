---
title: 返回 SQL_NO_DATA |Microsoft 文档
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
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9964b3a71797021b021fe8c97bd5261d81e3f023
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="returning-sqlnodata"></a>返回 SQL_NO_DATA
当一个 ODBC 2。*x*应用程序但 ODBC 3 *.x*驱动程序调用**SQLExecDirect**， **SQLExecute**，或**SQLParamData**，和搜索的更新或删除语句已执行，但未影响任何行在数据源，ODBC 3 *.x*驱动程序应返回 SQL_SUCCESS。 当 ODBC 3 *.x*应用程序使用 ODBC 3 *.x*驱动程序调用**SQLExecDirect**， **SQLExecute**，或**SQLParamData**与相同的结果，ODBC 3 *.x*驱动程序应返回 SQL_NO_DATA。  
  
 如果搜索的更新或删除语句中的一批语句不会影响数据源中的任何行**SQLMoreResults**返回 SQL_SUCCESS。 它不能返回 SQL_NO_DATA，因为这可能意味着有更多结果，不是有搜索更新/删除影响任何行从一个结果。
