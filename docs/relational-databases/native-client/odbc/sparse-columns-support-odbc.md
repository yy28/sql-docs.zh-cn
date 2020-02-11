---
title: 稀疏列支持（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f5fa48a2ddeb884611b86387e1ea044cf865639
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73760628"
---
# <a name="sparse-columns-support-odbc"></a>稀疏列支持 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主题描述对稀疏列的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 支持。 有关演示 ODBC 对稀疏列的支持的示例，请参阅对[具有稀疏列的表调用 SQLColumns](../../../relational-databases/native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md)。 有关稀疏列的详细信息，请参阅[SQL Server Native Client 中的稀疏列支持](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)。  
  
## <a name="statement-metadata"></a>语句元数据  
 应用程序参数描述符 (APD) 字段和 SQL_SOPT_SS_NAME_SCOPE 语句属性接受新增的值 SQL_SS_NAME_SCOPE_EXTENDED 和 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET。 这些值指定由[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)返回的结果集中包含的列。 有关 SQL_SOPT_SS_NAME_SCOPE 的详细信息，请参阅[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 新的实现行描述符（IRD）是一个名为 SQL_CA_SS_IS_COLUMN_SET 的只读 SQLSMALLINT 字段，可用于确定列是否为 XML **column_set**值。 SQL_CA_SS_IS_COLUMN_SET 接受值 SQL_TRUE 和 SQL_FALSE。  
  
## <a name="catalog-metadata"></a>目录元数据  
 已[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]将两个特定列（SS_IS_SPARSE 和 SS_IS_COLUMN_SET）添加到[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)的结果集中。  
  
## <a name="odbc-function-support-for-sparse-columns"></a>对稀疏列的 ODBC 函数支持  
 以下 ODBC 函数已进行更新，以便在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中支持稀疏列：  
  
-   [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
