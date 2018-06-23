---
title: SQLDescribeCol | Microsoft Docs
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
- SQLDescribeCol function
ms.assetid: ffbf34c6-8268-434f-829a-82009a6cda59
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c9c7a2471662efb547d8572ebb78a0a99646c20a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028145"
---
# <a name="sqldescribecol"></a>SQLDescribeCol
  对于执行语句， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序不需要查询服务器，以描述在结果集中的列。 在这种情况下，`SQLDescribeCol`不会导致服务器往返。 如[SQLColAttribute](sqlnumresultcols.md)，则调用`SQLDescribeCol`在准备好但是未执行的语句会生成服务器往返。  
  
 当某个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或语句批处理返回多个结果行集时，由序号引用的某一列可能来自单独的表或引用结果集中完全不同的列。 `SQLDescribeCol` 应为每个组调用。 如果结果集有变化，应用程序应该在提取行结果之前重新绑定数据值。 有关处理多个结果集返回，请参阅[SQLMoreResults](sqlmoreresults.md)。  
  
 当已准备的一批 SQL 语句生成多个结果集时，只为第一个结果集报告列属性。  
  
 对于大型值数据类型值将返回在*DataTypePtr*是 SQL_VARCHAR、 SQL_VARBINARY，还是 SQL_NVARCHAR。 值为在 SQL_SS_LENGTH_UNLIMITED *ColumnSizePtr*指示的大小是"无限制"。  
  
 从数据库引擎中的改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允许 SQLDescribeCol 以获取更准确的预期结果的说明。 这些更准确的结果可能与在以前版本的 SQLDescribeCol 返回的值不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../native-client/features/metadata-discovery.md)。  
  
## <a name="sqldescribecol-support-for-enhanced-date-and-time-features"></a>SQLDescribeCol 对日期和时间增强功能的支持  
 日期/时间类型返回以下值：  
  
||*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|---------------------|------------------------|  
|DATETIME|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|日期|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 有关详细信息，请参阅[日期和时间改进&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqldescribecol-support-for-large-clr-udts"></a>SQLDescribeCol 对大型 CLR UDT 的支持  
 `SQLDescribeCol` 支持大型 CLR 用户定义类型 (UDT)。 有关详细信息，请参阅[Large CLR User-Defined 类型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLDescribeCol 函数](http://go.microsoft.com/fwlink/?LinkID=59338)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  