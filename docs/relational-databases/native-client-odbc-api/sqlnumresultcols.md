---
title: SQLNumResultCols |微软文档
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2b56dad6564bad751829497117cc74553806b244
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302378"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  对于已执行的语句[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，本机客户端 ODBC 驱动程序不会访问服务器来报告结果集中的列数。 在这种情况下 **，SQLNumResultCols**不会导致服务器往返。 与[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)和[SQLColAttribute 一](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)样，在已准备好但未执行语句时调用**SQLNumResultCols**会生成服务器往返。  
  
 当某个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或语句批处理返回多个结果行集时，结果集列的个数可能在各个集之间有所变化。 应为每个集调用**SQLNumResultCols。** 如果列数有变化，应用程序应该在提取行结果之前重新绑定数据值。 有关处理多个结果集返回的详细信息，请参阅[SQLMore 结果](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 数据库引擎的改进从 SQLNumResultCols 开始[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，可以更精确地描述预期结果。 这些更准确的结果可能与 SQLNumResultCols 在 以前的版本中返回的值不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLNumResultCols 函数](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
