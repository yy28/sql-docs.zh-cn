---
title: SQLSpecialColumns |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 24661c0937c0af83d39831b60b535bd58ebcc626
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012379"
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  请求行标识符（*IdentifierType* SQL_BEST_ROWID）时， **SQLSpecialColumns**为除 SQL_SCOPE_CURROW 以外的任何请求的作用域返回空的结果集（无数据行）。 生成的结果集指示仅在此作用域内这些列有效。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持标识符的伪列。 **SQLSpecialColumns**结果集将所有列标识为 SQL_PC_NOT_PSEUDO。  
  
 可以对静态游标执行**SQLSpecialColumns** 。 尝试对可更新的（键集驱动或动态）执行**SQLSpecialColumns**将返回 SQL_SUCCESS_WITH_INFO 指示游标类型已更改。  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>SQLSpecialColumns 对日期和时间增强功能的支持  
 有关为日期/时间类型 DATA_TYPE、TYPE_NAME、COLUMN_SIZE、BUFFER_LENGTH 和 DECIMAL_DIGTS 返回的列的值的信息，请参阅[目录元数据](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 有关更多常规信息，请参阅[ODBC&#41;&#40;日期和时间改进](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>SQLSpecialColumns 对大型 CLR UDT 的支持  
 **SQLSpecialColumns**支持大型 CLR 用户定义类型（udt）。 有关详细信息，请参阅[&#40;ODBC&#41;的大型 CLR 用户定义类型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLSpecialColumns 函数](https://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
