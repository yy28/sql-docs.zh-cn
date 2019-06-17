---
title: SQLPrimaryKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a12392f9e70fec2fae3b7790b43f12779b8868b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046671"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  一个表可能会有一列或可用作唯一的行标识符的列和表创建 PRIMARY KEY 约束没有返回空结果集为 SQLPrimaryKeys。 ODBC 函数[SQLSpecialColumns](sqlspecialcolumns.md)报告行标识符候选表没有主键。  
  
 SQLPrimaryKeys 是否存在值都返回 SQL_SUCCESS *CatalogName*， *SchemaName*，或*TableName*参数。 SQLFetch 返回 SQL_NO_DATA 时这些参数中使用的值无效。  
  
 SQLPrimaryKeys 可以对静态服务器游标执行。 尝试对可更新的 （动态或键集） 游标执行 SQLPrimaryKeys 将返回 sql_success_with_info 以指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序通过接受由两部分名称来支持链接服务器上的表报告信息*CatalogName*参数：*Linked_Server_Name.Catalog_Name*。  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys 和表值参数  
 如果语句属性 SQL_SOPT_SS_NAME_SCOPE 采用值 SQL_SS_NAME_SCOPE_TABLE_TYPE，而不是其默认值 SQL_SS_NAME_SCOPE_TABLE，SQLPrimaryKeys 将返回有关主键列的表类型的信息。 有关 SQL_SOPT_SS_NAME_SCOPE 的详细信息，请参阅[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLPrimaryKeys 函数](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
