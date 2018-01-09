---
title: "稀疏列支持 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|ODBC
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f65dd0111076a4d779d203519164902df4dc1eac
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="sparse-columns-support-odbc"></a>稀疏列支持 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  本主题描述对稀疏列的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 支持。 有关示例，演示对稀疏列的 ODBC 支持，请参阅[具有稀疏列的表上调用 SQLColumns](../../../relational-databases/native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md)。 有关稀疏列的详细信息，请参阅[中 SQL Server Native Client 的稀疏列支持](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)。  
  
## <a name="statement-metadata"></a>语句元数据  
 应用程序参数描述符 (APD) 字段和 SQL_SOPT_SS_NAME_SCOPE 语句属性接受新增的值 SQL_SS_NAME_SCOPE_EXTENDED 和 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET。 这些值指定哪些列包含在返回的结果集[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)。 有关 SQL_SOPT_SS_NAME_SCOPE 的详细信息，请参阅[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 新实现行描述符 (IRD)，一个名为 SQL_CA_SS_IS_COLUMN_SET，只读 SQLSMALLINT 字段可以用于确定列是否为 XML **column_set**值。 SQL_CA_SS_IS_COLUMN_SET 接受值 SQL_TRUE 和 SQL_FALSE。  
  
## <a name="catalog-metadata"></a>目录元数据  
 两个[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]特定列 （SS_IS_SPARSE 和 SS_IS_COLUMN_SET） 已添加到的结果集中[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)。  
  
## <a name="odbc-function-support-for-sparse-columns"></a>对稀疏列的 ODBC 函数支持  
 以下 ODBC 函数已进行更新，以便在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中支持稀疏列：  
  
-   [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client &#40; ODBC &#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
