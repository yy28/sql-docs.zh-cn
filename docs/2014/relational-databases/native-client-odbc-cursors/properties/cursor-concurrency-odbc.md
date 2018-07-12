---
title: 游标并发 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c5e18839b74637311edfba3cd75ac3f4dfd7214
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408346"
---
# <a name="cursor-concurrency-odbc"></a>游标并发 (ODBC)
  和游标类型一样，游标操作也受应用程序设置的并发选项的影响。 使用的 SQL_ATTR_CONCURRENCY 选项设置并发选项[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)。 并发类型包括：  
  
-   只读 (SQL_CONCUR_READONLY)  
  
-   值 (SQL_CONCUR_VALUES)  
  
-   行版本 (SQL_CONCUR_ROWVER)  
  
-   锁 (SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>请参阅  
 [游标属性](cursor-properties.md)  
  
  
