---
title: 仅快进光标 （ODBC） |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 50d79875e0f3f661c0a959f50ce68c4f2761d186
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298411"
---
# <a name="fast-forward-only-cursors-odbc"></a>快速只进游标 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  连接到 的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序支持仅转发、只读游标的性能优化。 快速只进游标由驱动程序和服务器采用近似于默认结果集的方式在内部实现。 除高性能之外，快速只进游标还具有以下特征：  
  
-   [不支持 SQLGet 数据](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)。 结果集列必须绑定到程序变量。  
  
-   当检测到达游标末尾时，服务器自动关闭游标。 应用程序仍必须调用[SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md)或[SQLFreeStmt（SQL_CLOSE），](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)但驱动程序不必将关闭的请求发送到服务器。 这就省去了通过网络往返服务器。  
  
 应用程序使用驱动程序特定的语句属性 SQL_SOPT_SS_CURSOR_OPTIONS 请求快速只进游标。 如果设置为 SQL_CO_FFO，则启用快速只进游标，不启用自动提取。 如果设置为 SQL_CO_FFO_AF，则同时启用自动提取选项。 有关自动提取的详细信息，请参阅使用[ODBC 光标使用自动提取](../../../relational-databases/native-client-odbc-cursors/programming/using-autofetch-with-odbc-cursors.md)。  
  
 启用了自动提取的快速只进游标可用于检索较小的结果集，只需进行一次服务器往返。 在这些步骤中 *，n*是要返回的行数：  
  
1.  将 SQL_SOPT_SS_CURSOR_OPTIONS 设置为 SQL_CO_FFO_AF。  
  
2.  将SQL_ATTR_ROW_ARRAY_SIZE设置为*n* = 1。  
  
3.  将结果列绑定到*n* = 1 元素的数组（如果实际提取*了 n* = 1 行，则要安全）。  
  
4.  使用**SQLExecDirect**或**SQLExecute**打开光标。  
  
5.  如果返回状态为SQL_SUCCESS，则调用**SQLFreeStmt**或**SQLCloseCursor**关闭光标。 所有行数据将位于绑定程序变量中。  
  
 通过这些步骤 **，SQLExecDirect**或**SQLExecute**会在启用自动提取选项后发送游标打开请求。 对于来自客户端的单个请求，服务器执行以下操作：  
  
-   打开游标。  
  
-   生成结果集并将行发送给客户端。  
  
-   由于行集大小设置为比结果集中的行数大 1，因此服务器检测到游标末尾并关闭游标。  
  
## <a name="see-also"></a>另请参阅  
 [光标编程详细信息&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
