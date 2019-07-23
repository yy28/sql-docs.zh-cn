---
title: 从 SQL Server 2005 Native Client 更新应用程序 | Microsoft Docs
description: 从 SQL Server 2005 Native Client 更新应用程序
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 7915b9fb74f05057e05eef022d7f9b0e4ccdd21f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989256"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>从 SQL Server 2005 Native Client 更新应用程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本主题讨论了中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]的 Native Client 后 OLE DB Driver for SQL Server 中的重大更改。  

 从 Microsoft 数据访问组件 (MDAC) 升级到适用于 SQL Server 的 OLE DB 驱动程序时，也会看到一些行为差异。 有关详细信息, 请参阅[将应用程序更新为从 MDAC SQL Server OLE DB 驱动程序](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 随 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 附带。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 随 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 附带。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 随 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 附带。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 随 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 附带。  

|与[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 相比 SQL Server 的 OLE DB 驱动程序中更改的行为|描述|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB 仅填充到定义的小数位数。|对于将转换的数据发送到服务器的转换, OLE DB 的驱动程序 SQL Server 填充数据中的尾随零, 最大长度为**日期时间**值的最大长度。 SQL Server Native Client 9.0 则填充到 9 位数。|  
|验证 DBTYPE_DBTIMESTAMP for ICommandWithParameter:: SetParameterInfo。|SQL Server 的 OLE DB 驱动程序实现了 ICommandWithParameter:: SetParameterInfo 中*bScale*的 OLE DB 要求, 将设置为 DBTYPE_DBTIMESTAMP 的秒小数部分。|  
|对于 IS_NULLABLE 列, **sp_columns**存储过程现在返回 **"no"** , 而不是 **"no** "。|在 SQL Server OLE DB 驱动程序中, **sp_columns**存储过程现在为 IS_NULLABLE 列返回 **"no"** , 而不是 **"no"** 。|  
|日期超出范围时返回其他错误。|对于**日期时间**类型, 与早期版本中返回的超出范围日期的 SQL Server OLE DB 驱动程序将返回不同的错误号。<br /><br /> 具体来说[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , Native Client 9.0 在字符串转换为**datetime**时, 为所有超出范围的年份值返回 22007, SQL Server OLE DB 而当日期在**datetime2**支持的范围内但在外部时返回22008。**datetime**或**smalldatetime**支持的范围。|  
|如果舍入将更改日期，则 datetime 值将截断秒的小数部分，并且不舍入  。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，对于发送到服务器的 datetime 值的客户端行为是将它们舍入到最接近 1/300 秒的值  。 在 SQL Server OLE DB 驱动程序中, 如果舍入更改日期, 则此方案会导致截断秒的小数部分。|  
|**Datetime**值的可能的且。|如果绑定到某一 datetime 列并且其类型标识符为 DBTYPE_DBTIMESTAMP (OLE DB) 或 SQL_TIMESTAMP (ODBC)、小数位数为 0，则使用连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 服务器的适用于 SQL Server 的 OLE DB 驱动程序生成的应用程序将截断要发送到服务器的时间部分中的秒和秒的小数部分。<br /><br /> 例如：<br /><br /> 输入数据：1994-08-21 21:21:36.000<br /><br /> 插入的数据：1994-08-21 21:21:00.000|  
|从 DBTYPE_DBTIME 到 DBTYPE_DATE 的 OLE DB 数据转换不会再导致日期发生更改。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，如果 DBTYPE_DATE 的时间部分是在距离午夜的半秒内，则 OLE DB 转换代码将导致日期发生更改。 在 SQL Server OLE DB 驱动程序中, 日期不会更改 (秒的小数部分将被截断, 并且不会进行舍入)。|  
|IBCPSession:: BCColFmt 转换更改。|在 SQL Server OLE DB 驱动程序中, 当你使用 IBCPSession:: BCOColFmt 将 SQLDATETIME 或 SQLDATETIME 转换为字符串类型时, 将导出小数值。 例如，将类型 SQLDATETIME 转换为类型 SQLNVARCHARMAX 时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前的版本返回<br /> 1989-02-01 00:00:00。<br />适用于 SQL Server 的 OLE DB 驱动程序返回 <br />1989-02-01 00:00:00.0000000。|  
|使用 BCP API 的自定义应用程序现在可以看到警告。|对于所有类型，如果数据长度超过某字段的指定长度，则 BCP API 将生成警告消息。 以前，该警告仅针对字符类型，而不会针对所有类型发出。|  
|将空字符串插入到绑定为日期/时间类型的 sql_variant 中会生成错误  。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 中，将空字符串插入到绑定为日期/时间类型的 sql_variant 中不会生成错误  。 SQL Server 的 OLE DB 驱动程序在这种情况下会生成错误。|  
|当有触发器运行时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可能会返回不同的结果。|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中引入的变化可能会导致应用程序得到从 NOCOUNT OFF 有效时导致触发器运行的语句返回的不同的结果  。 在这种情况下，您的应用程序可能会生成错误。 若要解决此错误, 请在触发器中将 NOCOUNT 设置为**ON** 。|  

## <a name="see-also"></a>另请参阅   
 [适用于 SQL Server 的 OLE DB 驱动程序](../../oledb/oledb-driver-for-sql-server.md)
