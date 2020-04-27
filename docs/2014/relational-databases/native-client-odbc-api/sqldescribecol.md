---
title: SQLDescribeCol |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDescribeCol function
ms.assetid: ffbf34c6-8268-434f-829a-82009a6cda59
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95d367efc0bf3fb3e3a74bd0ba9d48b9d8f25be2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067763"
---
# <a name="sqldescribecol"></a>SQLDescribeCol
  对于已执行的语句[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，NATIVE Client ODBC 驱动程序不需要查询服务器来描述结果集中的列。 在这种情况`SQLDescribeCol`下，不会导致服务器往返。 与[SQLColAttribute](sqlnumresultcols.md)一样， `SQLDescribeCol`对已准备但未执行的语句调用会生成服务器往返。  
  
 当某个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或语句批处理返回多个结果行集时，由序号引用的某一列可能来自单独的表或引用结果集中完全不同的列。 `SQLDescribeCol`应为每个集调用。 如果结果集有变化，应用程序应该在提取行结果之前重新绑定数据值。 有关处理多个结果集返回的详细信息，请参阅[SQLMoreResults](sqlmoreresults.md)。  
  
 当已准备的一批 SQL 语句生成多个结果集时，只为第一个结果集报告列属性。  
  
 对于大值数据类型，在*DataTypePtr*中返回的值为 SQL_VARCHAR、SQL_VARBINARY 或 SQL_NVARCHAR。 *ColumnSizePtr*中的值 SQL_SS_LENGTH_UNLIMITED 指示大小为 "无限制"。  
  
 从 " [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允许 SQLDescribeCol" 开始，数据库引擎中的改进可获取预期结果的更准确说明。 更准确的结果可能与早期版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQLDescribeCol 返回的值不同。 有关详细信息，请参阅[元数据发现](../native-client/features/metadata-discovery.md)。  
  
## <a name="sqldescribecol-support-for-enhanced-date-and-time-features"></a>SQLDescribeCol 对日期和时间增强功能的支持  
 日期/时间类型返回以下值：  
  
||*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|---------------------|------------------------|  
|日期/时间|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19、21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26、28..34|0..7|  
  
 有关详细信息，请参阅[ODBC&#41;&#40;日期和时间改进](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqldescribecol-support-for-large-clr-udts"></a>SQLDescribeCol 对大型 CLR UDT 的支持  
 `SQLDescribeCol` 支持大型 CLR 用户定义类型 (UDT)。 有关详细信息，请参阅[&#40;ODBC&#41;的大型 CLR 用户定义类型](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLDescribeCol 函数](https://go.microsoft.com/fwlink/?LinkID=59338)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
