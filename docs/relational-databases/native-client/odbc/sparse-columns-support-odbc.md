---
title: 稀疏列支持 (ODBC) |Microsoft Docs
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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6ff1b60e1fec128da9c78ca6e0b909fbd5f0911a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47638926"
---
# <a name="sparse-columns-support-odbc"></a>稀疏列支持 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  本主题描述对稀疏列的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 支持。 演示对稀疏列 ODBC 支持的示例，请参阅[对具有稀疏列的表调用 SQLColumns](../../../relational-databases/native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md)。 有关稀疏列的详细信息，请参阅[SQL Server Native Client 中的稀疏列支持](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)。  
  
## <a name="statement-metadata"></a>语句元数据  
 应用程序参数描述符 (APD) 字段和 SQL_SOPT_SS_NAME_SCOPE 语句属性接受新增的值 SQL_SS_NAME_SCOPE_EXTENDED 和 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET。 这些值指定哪些列包含在返回的结果集[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)。 有关 SQL_SOPT_SS_NAME_SCOPE 的详细信息，请参阅[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 新的实现行描述符 (IRD)，一个名为 SQL_CA_SS_IS_COLUMN_SET，只读 SQLSMALLINT 字段可用于确定列是否为 XML **column_set**值。 SQL_CA_SS_IS_COLUMN_SET 接受值 SQL_TRUE 和 SQL_FALSE。  
  
## <a name="catalog-metadata"></a>目录元数据  
 两个[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]特定列 （SS_IS_SPARSE 和 SS_IS_COLUMN_SET） 已添加到结果集中[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)。  
  
## <a name="odbc-function-support-for-sparse-columns"></a>对稀疏列的 ODBC 函数支持  
 以下 ODBC 函数已进行更新，以便在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中支持稀疏列：  
  
-   [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
