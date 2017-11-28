---
title: "更新应用程序从 SQL Server 2005 的本机客户端 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
caps.latest.revision: "42"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bde56c3efe2231d54463c4d23f311237415a6f53
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>从 SQL Server 2005 Native Client 更新应用程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  本主题介绍自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 以来在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 中的重大更改。  
  
 从 Microsoft 数据访问组件 (MDAC) 升级到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 时，也会看到一些行为差异。 有关详细信息，请参阅[更新到 SQL Server Native Client 应用程序从 MDAC](../../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 9.0 附带[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 附带[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 随 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 附带。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 随 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 附带。  
  
|自 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以来 SQL Server Native Client 中已更改的行为|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB 仅填充到定义的小数位数。|转换其中转换的数据发送到服务器，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 (从[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 填充尾随仅之前的最大长度的数据中的零**datetime**值。 SQL Server Native Client 9.0 则填充到 9 位数。|  
|验证 ICommandWithParameter::SetParameterInfo DBTYPE_DBTIMESTAMP。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 (从[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 实现的 OLE DB 要求*bScale*中 ICommandWithParameter::SetParameterInfo 以设 DBTYPE_DBTIMESTAMP 秒的小数部分的精度。|  
|**Sp_columns**存储过程现在返回**"否"**而不是**"否"** IS_NULLABLE 列。|从[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)])， **sp_columns**存储过程现在返回**"否"**而不是**"否"** IS_NULLABLE 列.|  
|SQLSetDescRec、 SQLBindParameter 和 SQLBindCol 现在执行一致性检查。|之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0，设置 SQL_DESC_DATA_PTR 不会在 SQLSetDescRec、 SQLBindParameter 或 SQLBindCol 导致任何描述符类型的一致性检查。|  
|SQLCopyDesc 现在执行描述符一致性检查。|之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0，SQLCopyDesc 未执行操作一致性检查特定的记录上设置 SQL_DESC_DATA_PTR 字段时。|  
|SQLGetDescRec 不再不描述符一致性检查。|之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0，当设置了 SQL_DESC_DATA_PTR 字段 SQLGetDescRec 执行描述符一致性检查。 这不是 ODBC 规范和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 以及更高版本所要求的，该一致性检查不再执行。|  
|日期超出范围时返回其他错误。|有关**datetime**类型，将通过返回不同的错误号[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 (从[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 的范围外的日期不是在早期版本中返回。<br /><br /> 具体而言，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 9.0 所有超出范围中的字符串转换到的年份值返回 22007 **datetime**，和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端版本 10.0 开头 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 返回 22008 在日期是在支持的范围内**datetime2**但在支持范围之内**datetime**或**smalldatetime**。|  
|**datetime**值将截断秒的小数部分，并且不 round 如果舍入将会更改在一天。|之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0，供客户端行为**datetime**发送到服务器的值是四舍五入为最接近的 1/300 秒。 从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 开始，如果舍入会更改日期，则该方案会导致截断秒的小数部分。|  
|可能的秒 trunction **datetime**值。|如果您绑定到某一 datetime 列并且其类型标识符为 DBTYPE_DBTIMESTAMP (OLE DB) 或 SQL_TIMESTAMP (ODBC)、小数位数为 0，则使用连接到 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 2005 服务器的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client（或更高版本）生成的应用程序将截断要发送到服务器的时间部分中的秒和秒的小数部分。<br /><br /> 例如：<br /><br /> 输入数据：1994-08-21 21:21:36.000<br /><br /> 插入的数据：1994-08-21 21:21:00.000|  
|从 DBTYPE_DBTIME 到 DBTYPE_DATE 的 OLE DB 数据转换不会再导致日期发生更改。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，如果 DBTYPE_DATE 的时间部分是在距离午夜的半秒内，则 OLE DB 转换代码将导致日期发生更改。 从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 开始，日期不会更改（秒的小数部分将截断但不舍入）。|  
|IBCPSession::BCColFmt 转换更改。|从[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]导出 Native Client 10.0，当你使用 IBCPSession::BCOColFmt 将 SQLDATETIME 或 SQLDATETIME 转换为字符串类型，小数部分值。 例如，将类型 SQLDATETIME 转换为类型 SQLNVARCHARMAX 时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的更早版本返回<br /><br /> 1989-02-01 00:00:00. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 及更高版本返回 1989-02-01 00:00:00.0000000。|  
|发送的数据的大小必须与 SQL_LEN_DATA_AT_EXEC 中指定的长度匹配。|使用 SQL_LEN_DATA_AT_EXEC 时，数据的大小必须与用 SQL_LEN_DATA_AT_EXEC 指定的长度匹配。 可以使用 SQL_DATA_AT_EXEC，但使用 SQL_LEN_DATA_AT_EXEC 有潜在的性能好处。|  
|使用 BCP API 的自定义应用程序现在可以看到警告。|对于所有类型，如果数据长度超过某字段的指定长度，则 BCP API 将生成警告消息。 以前，该警告仅针对字符类型，而不会针对所有类型发出。|  
|插入到空字符串**sql_variant**绑定是日期/时间类型生成错误。|在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 9.0，插入到空字符串**sql_variant**绑定日期/时间类型未生成错误。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0（和更高版本）在这种情况下则会正确地生成错误。|  
|更严格的 SQL_C_TYPE _TIMESTAMP 和 DBTYPE_DBTIMESTAMP 参数验证。|之前[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]Native Client， **datetime**已舍入值以适合的规模**datetime**和**smalldatetime**列 × [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client（和更高版本）现在应用在 ODBC 核心规范中为秒的小数部分定义的更严格的验证规则。 如果无法通过使用由客户端绑定所指定或暗含的小数位数在不截断尾随数字的情况下将参数值转换到 SQL 类型，则返回错误。|  
|当有触发器运行时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可能会返回不同的结果。|在中引入的更改[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]可能会导致应用程序具有不同的结果从导致触发器时要运行的语句返回**NOCOUNT OFF**已起作用。 在这种情况下，您的应用程序可能会生成错误。 若要解决此错误，将设置**NOCOUNT ON**触发器或调用 SQLMoreResults 以转到下一个结果中。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 编程](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
