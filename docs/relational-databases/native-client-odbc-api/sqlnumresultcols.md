---
description: SQLNumResultCols
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2f4f868d9e32aa553930929cc0f713c9cc29136c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424029"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  对于执行的语句， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驱动程序不会访问服务器来报告结果集中的列数。 在这种情况下， **SQLNumResultCols** 不会导致服务器往返。 与 [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 和 [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)类似，在已准备但未执行的语句上调用 **SQLNumResultCols** 将生成服务器往返。  
  
 当某个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或语句批处理返回多个结果行集时，结果集列的个数可能在各个集之间有所变化。 应对每个集都调用**SQLNumResultCols** 。 如果列数有变化，应用程序应该在提取行结果之前重新绑定数据值。 有关处理多个结果集返回的详细信息，请参阅 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 从 "允许 SQLNumResultCols" 开始，数据库引擎中的改进 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 可获取预期结果的更准确说明。 更准确的结果可能与早期版本的 SQLNumResultCols 返回的值不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 有关详细信息，请参阅[元数据发现](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLNumResultCols 函数](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
