---
title: SQLPrimaryKeys |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cb0dc440025730c278206a751a5ce741b69b0f6e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016604"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  表可能具有一列或可用作唯一行标识符的列，而无需 PRIMARY KEY 约束创建的表返回空结果设置为 SQLPrimaryKeys。 ODBC 函数[SQLSpecialColumns](sqlspecialcolumns.md)报表行的没有主键的表的标识符候选项。  
  
 SQLPrimaryKeys 是否值已存在，则返回 SQL_SUCCESS *CatalogName*， *SchemaName*，或*TableName*参数。 SQLFetch 返回 SQL_NO_DATA，在这些参数中使用了无效值。  
  
 SQLPrimaryKeys 可以执行对静态服务器游标。 尝试执行的可更新的 （动态或键集） 游标 SQLPrimaryKeys 将返回 SQL_SUCCESS_WITH_INFO 指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持为链接服务器上的表报表信息由接受的两部分名称*CatalogName*参数： *Linked_Server_Name.Catalog_Name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys 和表值参数  
 如果语句属性 SQL_SOPT_SS_NAME_SCOPE 具有值 SQL_SS_NAME_SCOPE_TABLE_TYPE，而不是 SQL_SS_NAME_SCOPE_TABLE 其默认值，SQLPrimaryKeys 将返回有关主键列的表类型的信息。 SQL_SOPT_SS_NAME_SCOPE 的详细信息，请参阅[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLPrimaryKeys 函数](http://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  