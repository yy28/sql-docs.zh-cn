---
title: SQLPrimaryKeys |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046671"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  表中可能有一列或多列可用作唯一的行标识符，而在没有 PRIMARY KEY 约束的情况下创建的表会将空结果集返回到 SQLPrimaryKeys。 ODBC 函数[SQLSpecialColumns](sqlspecialcolumns.md)报告没有主键的表的行标识符候选项。  
  
 SQLPrimaryKeys 返回 SQL_SUCCESS *CatalogName*、 *SchemaName*或*TableName*参数是否存在值。 当这些参数中使用的值无效时，SQLFetch 返回 SQL_NO_DATA。  
  
 可以对静态服务器游标执行 SQLPrimaryKeys。 尝试对可更新的（动态或键集）游标执行 SQLPrimaryKeys 时，将返回 SQL_SUCCESS_WITH_INFO，指示游标类型已更改。  
  
 Native Client ODBC 驱动程序通过接受由两部分组成的*CatalogName*参数的名称来支持链接服务器上表的报告信息： *Linked_Server_Name。 Catalog_Name。* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys 和表值参数  
 如果语句特性 SQL_SOPT_SS_NAME_SCOPE 的值 SQL_SS_NAME_SCOPE_TABLE_TYPE，而不是其默认值 SQL_SS_NAME_SCOPE_TABLE，则 SQLPrimaryKeys 将返回有关表类型的主键列的信息。 有关 SQL_SOPT_SS_NAME_SCOPE 的详细信息，请参阅[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 有关表值参数的详细信息，请参阅[ODBC&#41;&#40;表值参数](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLPrimaryKeys 函数](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
