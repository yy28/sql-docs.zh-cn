---
title: SQL 主键 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2695d253030f13f71785046a25997ec6ee768622
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288967"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  表可能具有可用作唯一行标识符的列或列，在没有"主要密钥"约束的情况下创建的表将空结果集返回到 SQLPrimaryKeys。 ODBC 函数[SQL 特别列](../../relational-databases/native-client-odbc-api/sqlspecialcolumns.md)报没有主键的表的行标识符候选项。  
  
 SQL 主要密钥SQL_SUCCESS*目录名称*、*架构名称*参数或*表名*参数是否存在值。 当这些参数中使用的值无效时，SQLFetch 返回 SQL_NO_DATA。  
  
 SQL主要密钥可以在静态服务器游标上执行。 尝试在可上升（动态或键集）游标上执行 SQLPrimaryKeys 将返回SQL_SUCCESS_WITH_INFO指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序通过接受*目录名称*参数的两部分名称 *（Linked_Server_Name.Catalog_Name*）支持报告链接服务器上的表的信息。  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys 和表值参数  
 如果语句属性SQL_SOPT_SS_NAME_SCOPE具有值SQL_SS_NAME_SCOPE_TABLE_TYPE，而不是其默认值SQL_SS_NAME_SCOPE_TABLE，SQLPrimaryKeys 将返回有关表类型的主要键列的信息。 有关SQL_SOPT_SS_NAME_SCOPE的详细信息，请参阅[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 有关表值参数的详细信息，请参阅[&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 主键函数](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
