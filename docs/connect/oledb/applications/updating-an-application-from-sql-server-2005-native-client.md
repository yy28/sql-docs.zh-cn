---
title: 从 SQL Server 2005 Native Client 更新应用程序 | Microsoft Docs
description: 从 SQL Server 2005 Native Client 更新应用程序
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 15d4f01dbf35385e1fba296e5d78e57fa35f16ed
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43034889"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>从 SQL Server 2005 Native Client 更新应用程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本主题讨论 OLE DB 驱动程序中的重大更改适用于 SQL Server 以来[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的本机客户端[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。  

 从 Microsoft 数据访问组件 (MDAC) 升级到适用于 SQL Server 的 OLE DB 驱动程序时，也会看到一些行为差异。 有关详细信息，请参阅[更新到 OLE DB 驱动程序的应用程序适用于 SQL Server 从 MDAC](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 随 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 附带。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 随 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 附带。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 随 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 附带。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 随 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 附带。  

|OLE DB 驱动程序中的行为更改适用于 SQL Server 相比[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]本机客户端|描述|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB 仅填充到定义的小数位数。|对于其中转换后的数据发送到服务器的转换，OLE DB 驱动程序适用于 SQL Server 来填充最多的最大长度的数据中的尾随零**datetime**值。 SQL Server Native Client 9.0 则填充到 9 位数。|  
|有关 ICommandWithParameter::SetParameterInfo 验证 DBTYPE_DBTIMESTAMP。|OLE DB 驱动程序适用于 SQL Server 实现的 OLE DB 要求*bScale*中 ICommandWithParameter::SetParameterInfo 到秒的小数部分精度设置为 DBTYPE_DBTIMESTAMP。|  
|**Sp_columns**存储过程现在返回 **"否"** 而不是 **"否"** 为 IS_NULLABLE 列。|OLE DB 驱动程序中的 SQL Server **sp_columns**存储过程现在返回 **"否"** 而不是 **"否"** 为 IS_NULLABLE 列。|  
|日期超出范围时返回其他错误。|有关**datetime**类型，不同的错误号将返回由 OLE DB 驱动程序适用于 SQL Server 超出范围日期比在早期版本中返回。<br /><br /> 具体而言， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 对所有字符串转换到的范围的年份值超出都返回 22007 **datetime**，和 OLE DB 驱动程序适用于 SQL Server 日期所支持的范围内时返回22008**datetime2**支持的范围但不**datetime**或**smalldatetime**。|  
|如果舍入将更改日期，则 datetime 值将截断秒的小数部分，并且不舍入。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，对于发送到服务器的 datetime 值的客户端行为是将它们舍入到最接近 1/300 秒的值。 OLE DB 驱动程序适用于 SQL Server，这种情况下会导致截断秒的小数部分，如果舍入会更改日期。|  
|秒的可能截断**datetime**值。|如果绑定到某一 datetime 列并且其类型标识符为 DBTYPE_DBTIMESTAMP (OLE DB) 或 SQL_TIMESTAMP (ODBC)、小数位数为 0，则使用连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 服务器的适用于 SQL Server 的 OLE DB 驱动程序生成的应用程序将截断要发送到服务器的时间部分中的秒和秒的小数部分。<br /><br /> 例如：<br /><br /> 输入数据：1994-08-21 21:21:36.000<br /><br /> 插入的数据：1994-08-21 21:21:00.000|  
|从 DBTYPE_DBTIME 到 DBTYPE_DATE 的 OLE DB 数据转换不会再导致日期发生更改。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，如果 DBTYPE_DATE 的时间部分是在距离午夜的半秒内，则 OLE DB 转换代码将导致日期发生更改。 OLE DB 驱动程序中的 SQL Server，日期不会更改 （截断秒的小数部分并且不进行舍入）。|  
|IBCPSession::BCColFmt 转换更改。|在 OLE DB 驱动程序适用于 SQL Server，在使用 IBCPSession::BCOColFmt 将 SQLDATETIME 或 SQLDATETIME 转换为字符串类型，被导出的小数部分值。 例如，将类型 SQLDATETIME 转换为类型 SQLNVARCHARMAX 时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前的版本返回<br /> 1989-02-01 00:00:00。<br />适用于 SQL Server 的 OLE DB 驱动程序返回 <br />1989-02-01 00:00:00.0000000。|  
|使用 BCP API 的自定义应用程序现在可以看到警告。|对于所有类型，如果数据长度超过某字段的指定长度，则 BCP API 将生成警告消息。 以前，该警告仅针对字符类型，而不会针对所有类型发出。|  
|将空字符串插入到绑定为日期/时间类型的 sql_variant 中会生成错误。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 中，将空字符串插入到绑定为日期/时间类型的 sql_variant 中不会生成错误。 OLE DB 驱动程序适用于 SQL Server 在这种情况下正确地生成错误。|  
|当有触发器运行时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可能会返回不同的结果。|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中引入的变化可能会导致应用程序得到从 NOCOUNT OFF 有效时导致触发器运行的语句返回的不同的结果。 在这种情况下，您的应用程序可能会生成错误。 若要解决此错误，将**NOCOUNT ON**在触发器中。|  

## <a name="see-also"></a>另请参阅   
 [适用于 SQL Server 的 OLE DB 驱动程序](../../oledb/oledb-driver-for-sql-server.md)
