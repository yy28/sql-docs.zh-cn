---
title: 元数据发现 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ec3c0f4f-f838-43ce-85f2-cf2761e2aac5
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5bb0c1c7b0ff489e5addff5bb84649984b97f527
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416256"
---
# <a name="metadata-discovery"></a>元数据发现
  中的元数据发现改进[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]允许[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端应用程序以确保从执行的查询返回的列或参数元数据是否与相同或兼容的元数据设置你前面指定的格式执行查询。 如果执行查询后返回的元数据与执行该查询之前指定的元数据格式不兼容，您将会收到错误。  
  
 在 bcp 和 ODBC 函数以及 IBCPSession 和 IBCPSession2 接口中，您现在可以指定延迟读取（延迟的元数据发现）以避免对查询输出操作执行元数据发现。 这样可以提高性能，并避免元数据发现失败。  
  
 如果您开发应用程序中使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的本机客户端[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]但连接到的服务器版本早于[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，元数据发现功能将对应于服务器的版本。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中增强了以下 bcp 函数，以提供改进的元数据发现：  
  
-   [bcp_columns](../../native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_getcolfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_readfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_setcolfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
 指定元数据格式使用时，还将看到性能的改进[bcp_setbulkmode](../../native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md)。  
  
 [bcp_control](../../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)有一个新的*eOption*控制 bcp_readfmt 的行为： `BCPDELAYREADFMT`。  
  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中增强了以下 ODBC 函数，以提供改进的元数据发现：  
  
-   [SQLNumResultCols](../../native-client-odbc-api/sqlnumresultcols.md)  
  
-   [SQLDescribeCol](../../native-client-odbc-api/sqldescribecol.md)  
  
-   [SQLNumParams](../../native-client-odbc-api/sqlnumparams.md)  
  
-   [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md)  
  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中增强了以下 OLE DB 成员函数，以提供改进的元数据发现：  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   Icommandwithparameters:: Getparameterinfo (请参阅[ICommandWithParameters](../../native-client-ole-db-interfaces/icommandwithparameters.md)有关详细信息)  
  
 指定使用 IBCPSession::BCPSetBulkMode 的元数据格式时，还将看到性能的改进  
  
 由于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中新增了两个存储过程，[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client 中的元数据发现功能才得以改进：  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
