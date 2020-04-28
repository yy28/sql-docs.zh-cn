---
title: 元数据发现 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: ec3c0f4f-f838-43ce-85f2-cf2761e2aac5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5d822362e9f9f7e70e4421056383aae8ddef03dc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303348"
---
# <a name="metadata-discovery"></a>元数据发现
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  中[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]的元数据发现改进[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]允许 Native Client 应用程序确保从执行查询返回的列或参数元数据与执行查询之前指定的元数据格式相同或与其兼容。 如果执行查询后返回的元数据与执行该查询之前指定的元数据格式不兼容，您将会收到错误。  
  
 在 bcp 和 ODBC 函数以及 IBCPSession 和 IBCPSession2 接口中，您现在可以指定延迟读取（延迟的元数据发现）以避免对查询输出操作执行元数据发现。 这样可以提高性能，并避免元数据发现失败。  
  
 如果使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]的 Native Client 开发应用程序，但连接到早于[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]的服务器版本，则元数据发现功能将与服务器版本相对应。  
  
## <a name="remarks"></a>备注  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中增强了以下 bcp 函数，以提供改进的元数据发现：  
  
-   [bcp_columns](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_getcolfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_readfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_setcolfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
 使用[bcp_setbulkmode](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md)指定元数据格式时，您也会看到性能有所提高。  
  
 [bcp_control](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)提供了一个新的*eOption*来控制 bcp_readfmt： **BCPDELAYREADFMT**的行为。  
  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中增强了以下 ODBC 函数，以提供改进的元数据发现：  
  
-   [SQLNumResultCols](../../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)  
  
-   [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md)  
  
-   [SQLNumParams](../../../relational-databases/native-client-odbc-api/sqlnumparams.md)  
  
-   [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md)  
  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中增强了以下 OLE DB 成员函数，以提供改进的元数据发现：  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters::GetParameterInfo（有关详细信息，请参阅 [ICommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)）  
  
 使用 IBCPSession::BCPSetBulkMode 指定元数据格式时，也会看到性能改进  
  
 由于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中新增了两个存储过程，[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client 中的元数据发现功能才得以改进：  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
