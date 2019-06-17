---
title: 游标并发 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5c11ee87fe49e13bddd1a4331258a412916373b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63014219"
---
# <a name="cursor-concurrency-odbc"></a>游标并发 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  和游标类型一样，游标操作也受应用程序设置的并发选项的影响。 使用的 SQL_ATTR_CONCURRENCY 选项设置并发选项[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。 并发类型包括：  
  
-   只读 (SQL_CONCUR_READONLY)  
  
-   值 (SQL_CONCUR_VALUES)  
  
-   行版本 (SQL_CONCUR_ROWVER)  
  
-   锁 (SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>请参阅  
 [游标属性](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
