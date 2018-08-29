---
title: 从 SQL Server 2005 Native Client 更新应用程序 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 029c3be142a2b0882619a0612c66e72eef3d9eef
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43081833"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>从 SQL Server 2005 Native Client 更新应用程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  本主题介绍自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 以来在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 中的重大更改。  
  
 从 Microsoft 数据访问组件 (MDAC) 升级到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 时，也会看到一些行为差异。 有关详细信息，请参阅[更新到 SQL Server Native Client 应用程序从 MDAC](../../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 随 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 附带。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 随 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 附带。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 随 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 附带。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 随 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 附带。  
  
|自 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以来 SQL Server Native Client 中已更改的行为|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB 仅填充到定义的小数位数。|转换，转换后的数据发送到服务器， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (从[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 面板中的数据最多的最大长度仅尾随零**datetime**值。 SQL Server Native Client 9.0 则填充到 9 位数。|  
|有关 ICommandWithParameter::SetParameterInfo 验证 DBTYPE_DBTIMESTAMP。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 本机客户端 (从[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 实现的 OLE DB 要求*bScale*中 ICommandWithParameter::SetParameterInfo 到秒的小数部分精度设置为 DBTYPE_DBTIMESTAMP。|  
|**Sp_columns**存储过程现在返回 **"否"** 而不是 **"否"** 为 IS_NULLABLE 列。|从开始[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)])， **sp_columns**存储过程现在返回 **"否"** 而不是 **"否"** 为 IS_NULLABLE 列.|  
|SQLSetDescRec、 SQLBindParameter 和 SQLBindCol 现在执行一致性检查。|早于[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 中，设置 SQL_DESC_DATA_PTR 不会在 SQLSetDescRec、 SQLBindParameter 或 SQLBindCol 导致一致性检查的任何描述符类型。|  
|SQLCopyDesc 现在执行描述符一致性检查。|早于[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0，SQLCopyDesc 未不执行一致性检查，在特定记录上设置 SQL_DESC_DATA_PTR 字段时。|  
|SQLGetDescRec 不再不描述符一致性检查。|早于[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 中，设置 SQL_DESC_DATA_PTR 字段时 SQLGetDescRec 执行描述符一致性检查。 这不是 ODBC 规范和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 以及更高版本所要求的，该一致性检查不再执行。|  
|日期超出范围时返回其他错误。|有关**datetime**类型，将通过返回不同的错误号[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client (从[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 对范围扩展日期在早期版本中返回与。<br /><br /> 具体而言， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 对所有字符串转换到的范围的年份值超出都返回 22007 **datetime**，和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端从版本 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 返回 22008 时在日期处于支持的范围**datetime2**支持的范围但不**datetime**或**smalldatetime**。|  
|如果舍入将更改日期，则 datetime 值将截断秒的小数部分，并且不舍入。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，对于发送到服务器的 datetime 值的客户端行为是将它们舍入到最接近 1/300 秒的值。 从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 开始，如果舍入会更改日期，则该方案会导致截断秒的小数部分。|  
|秒的可能截断**datetime**值。|如果您绑定到某一 datetime 列并且其类型标识符为 DBTYPE_DBTIMESTAMP (OLE DB) 或 SQL_TIMESTAMP (ODBC)、小数位数为 0，则使用连接到 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 2005 服务器的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client（或更高版本）生成的应用程序将截断要发送到服务器的时间部分中的秒和秒的小数部分。<br /><br /> 例如：<br /><br /> 输入数据：1994-08-21 21:21:36.000<br /><br /> 插入的数据：1994-08-21 21:21:00.000|  
|从 DBTYPE_DBTIME 到 DBTYPE_DATE 的 OLE DB 数据转换不会再导致日期发生更改。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，如果 DBTYPE_DATE 的时间部分是在距离午夜的半秒内，则 OLE DB 转换代码将导致日期发生更改。 从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 开始，日期不会更改（秒的小数部分将截断但不舍入）。|  
|IBCPSession::BCColFmt 转换更改。|从[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]导出 Native Client 10.0，当你使用 IBCPSession::BCOColFmt 将 SQLDATETIME 或 SQLDATETIME 转换为字符串类型，小数部分值。 例如，将类型 SQLDATETIME 转换为类型 SQLNVARCHARMAX 时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的更早版本返回<br /><br /> 1989-02-01 00:00:00. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 及更高版本返回 1989-02-01 00:00:00.0000000。|  
|发送的数据的大小必须与 SQL_LEN_DATA_AT_EXEC 中指定的长度匹配。|使用 SQL_LEN_DATA_AT_EXEC 时，数据的大小必须与用 SQL_LEN_DATA_AT_EXEC 指定的长度匹配。 可以使用 SQL_DATA_AT_EXEC，但使用 SQL_LEN_DATA_AT_EXEC 有潜在的性能好处。|  
|使用 BCP API 的自定义应用程序现在可以看到警告。|对于所有类型，如果数据长度超过某字段的指定长度，则 BCP API 将生成警告消息。 以前，该警告仅针对字符类型，而不会针对所有类型发出。|  
|将空字符串插入到绑定为日期/时间类型的 sql_variant 中会生成错误。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 中，将空字符串插入到绑定为日期/时间类型的 sql_variant 中不会生成错误。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0（和更高版本）在这种情况下则会正确地生成错误。|  
|更严格的 SQL_C_TYPE _TIMESTAMP 和 DBTYPE_DBTIMESTAMP 参数验证。|早于[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]Native Client **datetime**值舍入，以适合的小数位数**datetime**和**smalldatetime**按列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client（和更高版本）现在应用在 ODBC 核心规范中为秒的小数部分定义的更严格的验证规则。 如果无法通过使用由客户端绑定所指定或暗含的小数位数在不截断尾随数字的情况下将参数值转换到 SQL 类型，则返回错误。|  
|当有触发器运行时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可能会返回不同的结果。|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中引入的变化可能会导致应用程序得到从 NOCOUNT OFF 有效时导致触发器运行的语句返回的不同的结果。 在这种情况下，您的应用程序可能会生成错误。 若要解决此错误，将**NOCOUNT ON**触发器或调用 SQLMoreResults 可以前进到下一步的结果中。|  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 编程](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
