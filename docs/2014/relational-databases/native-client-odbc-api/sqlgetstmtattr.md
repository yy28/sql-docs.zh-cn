---
title: SQLGetStmtAttr |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/25/2020
ms.locfileid: "62657806"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序扩展 SQLGetStmtAttr 以公开特定于驱动程序的语句属性。  
  
 [SQLSetStmtAttr](sqlsetstmtattr.md)列出了读写属性。 本主题列出只读语句属性。  
  
## <a name="sql_sopt_ss_current_command"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 SQL_SOPT_SS_CURRENT_COMMAND 属性公开命令批处理中的当前命令。 返回一个整数，该整数指定该命令在批处理中的位置。 *将 valueptr*值的类型为 SQLLEN。  
  
## <a name="sql_sopt_ss_nocount_status"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 SQL_SOPT_SS_NOCOUNT_STATUS 特性指示 NOCOUNT 选项的当前设置，该选项控制在调用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQLRowCount](sqlrowcount.md)时是否报告受语句影响的行数。 *将 valueptr*值的类型为 SQLLEN。  
  
|“值”|描述|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT 为 OFF。 SQLRowCount 返回受影响的行数。|  
|SQL_NC_ON|NOCOUNT 为 ON。 SQLRowCount 不返回受影响的行数，返回值为0。|  
  
 如果 SQLRowCount 返回0，则应用程序应测试 SQL_SOPT_SS_NOCOUNT_STATUS。 如果返回 SQL_NC_ON，则 SQLRowCount 的值将仅指示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]未返回行计数。 如果返回了 SQL_NC_OFF，则表示 NOCOUNT 为 off，并且 SQLRowCount 返回的 0 值表示该语句未影响任何行。  
  
 当 SQL_SOPT_SS_NOCOUNT_STATUS 为 SQL_NC_OFF 时，应用程序不应显示 SQLRowCount 的值。 大型批处理或存储过程可能包含多个 SET NOCOUNT 语句，所以不能认定 SQL_SOPT_SS_NOCOUNT_STATUS 保持不变。 每次 SQLRowCount 返回0时，应测试此选项。  
  
## <a name="sql_sopt_ss_querynotification_msgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 属性返回查询通知请求的消息文本。  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr 和表值参数  
 使用表值参数时，可以调用 SQLGetStmtAttr 来获取应用程序参数描述符（APD）中 SQL_SOPT_SS_PARAM_FOCUS 的值。 有关 SQL_SOPT_SS_PARAM_FOCUS 的详细信息，请参阅[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 有关表值参数的详细信息，请参阅[ODBC&#41;&#40;表值参数](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLSetStmtAttr 函数](https://go.microsoft.com/fwlink/?LinkId=59370)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
