---
title: SQLExecute |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLExecute function
ms.assetid: 4d7db8b6-611f-4fe4-be85-2a407059de45
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 149e502bc98e6f6bce03ee9d9615561b9fc4cb8d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32942582"
---
# <a name="sqlexecute"></a>SQLExecute
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  如果： SQL_SOPT_SS_PARAM_FOCUS 没有设置为 0，SQLExecute 语句属性将返回 SQL_ERROR 和生成的诊断记录 SQLSTATE = HY024 和消息"无效的属性值： SQL_SOPT_SS_PARAM_FOCUS （必须在执行时的零）"。 : SQL_SOPT_SS_PARAM_FOCUS 有关的详细信息，请参阅[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
## <a name="remarks"></a>注释  
 有关表值参数的详细信息，请参阅[表值参数 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=80708)   
 [ODBC API 实现详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
