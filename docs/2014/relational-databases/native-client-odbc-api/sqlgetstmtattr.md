---
title: SQLGetStmtAttr | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetStmtAttr function
ms.assetid: e64f4f94-eb73-4477-9745-080b6cbdc751
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5604aafbbc8a6d77081e829269955c8b7600f4ee
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359920"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序通过扩展 SQLGetStmtAttr 公开特定于驱动程序的语句属性。  
  
 [SQLSetStmtAttr](sqlsetstmtattr.md)列表语句属性均为读取和写入。 本主题列出只读语句属性。  
  
## <a name="sqlsoptsscurrentcommand"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 SQL_SOPT_SS_CURRENT_COMMAND 属性公开命令批处理中的当前命令。 返回一个整数，该整数指定该命令在批处理中的位置。 *ValuePtr*的值为类型为 SQLLEN。  
  
## <a name="sqlsoptssnocountstatus"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 SQL_SOPT_SS_NOCOUNT_STATUS 属性指示 NOCOUNT 的当前设置选项，哪些控件是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]报告的语句所影响的行时[SQLRowCount](sqlrowcount.md)调用。 *ValuePtr*的值为类型为 SQLLEN。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT 为 OFF。 SQLRowCount 返回受影响行数。|  
|SQL_NC_ON|NOCOUNT 为 ON。 SQLRowCount 将不返回受影响的行数和返回的值为 0。|  
  
 如果 SQLRowCount 返回 0，则应用程序应测试 SQL_SOPT_SS_NOCOUNT_STATUS。 如果返回 SQL_NC_ON，从 SQLRowCount 0 的值仅指示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]未返回行计数。 如果返回 SQL_NC_OFF，则表示 NOCOUNT 为 off，并从 SQLRowCount 0 的值指示语句未影响任何行。  
  
 当 SQL_SOPT_SS_NOCOUNT_STATUS 为 SQL_NC_OFF 时，应用程序不应显示 SQLRowCount 的值。 大型批处理或存储过程可能包含多个 SET NOCOUNT 语句，所以不能认定 SQL_SOPT_SS_NOCOUNT_STATUS 保持不变。 此选项应测试每次 SQLRowCount 返回 0。  
  
## <a name="sqlsoptssquerynotificationmsgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 属性返回查询通知请求的消息文本。  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr 和表值参数  
 SQLGetStmtAttr 可以调用来使用表值参数时，获取应用程序参数描述符 (APD) 中的 SQL_SOPT_SS_PARAM_FOCUS 的值。 有关 SQL_SOPT_SS_PARAM_FOCUS 的详细信息，请参阅[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLSetStmtAttr 函数](https://go.microsoft.com/fwlink/?LinkId=59370)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
