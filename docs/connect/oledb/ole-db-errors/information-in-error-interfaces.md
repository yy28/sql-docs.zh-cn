---
title: 错误接口中的信息
description: OLE DB Driver for SQL Server 在 OLE DB 定义的错误接口 IErrorInfo、IErrorRecords 和 ISQLErrorInfo 中报告某些错误和状态信息。
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 023926ff67c85dcf8d95499b8281853bf7b3b1f3
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860007"
---
# <a name="information-in-error-interfaces"></a>错误接口中的信息
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  适用于 SQL Server 的 OLE DB 驱动程序在 OLE DB 定义的错误接口 IErrorInfo、IErrorRecords 和 ISQLErrorInfo 中报告某些错误和状态信息    。  
  
 OLE DB Driver for SQL Server 支持 IErrorInfo  成员函数，如下所示。  
  
|成员函数|说明|  
|---------------------|-----------------|  
|**GetDescription**|错误消息说明性字符串。|  
|**GetGUID**|定义错误的接口的 GUID。|  
|**GetHelpContext**|不支持。 始终返回零。|  
|**GetHelpFile**|不支持。 始终返回 NULL。|  
|**GetSource**|字符串“适用于 SQL Server 的 Microsoft OLE DB 驱动程序”。|  
  
 OLE DB Driver for SQL Server 支持使用者可用的 IErrorRecords  成员函数，如下所示。  
  
|成员函数|说明|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|使用有关错误的基本信息填充 ERRORINFO 结构。 ERRORINFO 结构包含标识错误的 HRESULT 返回值的成员、访问接口和该错误适用的接口。|  
|**GetCustomErrorObject**|返回对 ISQLErrorInfo 和 [ISQLServerErrorInfo](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15) 接口的引用  。|  
|**GetErrorInfo**|返回对 IErrorInfo 接口的引用  。|  
|**GetErrorParameters**|OLE DB Driver for SQL Server 不通过 GetErrorParameters  向使用者返回参数。|  
|**GetRecordCount**|可用错误记录的计数。|  
  
 OLE DB Driver for SQL Server 支持 ISQLErrorInfo::GetSQLInfo  参数，如下所示。  
  
|参数|说明|  
|---------------|-----------------|  
|pbstrSQLState |返回错误的 SQLSTATE 值。 SQLSTATE 值在 SQL-92、ODBC 和 ISO SQL 以及 API 规范中定义。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 OLE DB Driver for SQL Server 都未定义特定于实现的 SQLSTATE 值。|  
|plNativeError |返回 master.dbo.sysmessages 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 错误编号（如果存在）  。 在初始化 OLE DB Driver for SQL Server 数据源的尝试成功后，本机错误就可返回。 在尝试之前，OLE DB Driver for SQL Server 始终返回零。|  
  
## <a name="see-also"></a>另请参阅  
 [错误](../../oledb/ole-db-errors/errors.md)  
  
  
