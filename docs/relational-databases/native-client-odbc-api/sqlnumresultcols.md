---
title: SQLNumResultCols |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ee85a2373154efa7a8488961c40f5c714c8b0314
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68131268"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  对于执行的语句， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序并不访问服务器以报告结果集中的列数。 在这种情况下， **SQLNumResultCols**不会导致服务器往返。 像[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)并[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)，则调用**SQLNumResultCols**对准备但不是执行的语句产生服务器往返。  
  
 当某个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或语句批处理返回多个结果行集时，结果集列的个数可能在各个集之间有所变化。 **SQLNumResultCols**应该为每个集调用。 如果列数有变化，应用程序应该在提取行结果之前重新绑定数据值。 有关详细信息，了解如何处理多个结果集返回，请参阅[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 从数据库引擎中的改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允许 SQLNumResultCols 若要获取的预期的结果更准确描述。 这些更准确的结果可能不同于 SQLNumResultCols 的早期版本中返回的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLNumResultCols 函数](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
