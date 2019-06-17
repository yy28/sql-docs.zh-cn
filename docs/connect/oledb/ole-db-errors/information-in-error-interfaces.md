---
title: 错误接口中的信息 |Microsoft Docs
description: 错误接口中的信息
ms.custom: ''
ms.date: 06/14/2018
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
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 7b87011fc8d95d617562bb72ce6a3a6ee49ae0c5
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798129"
---
# <a name="information-in-error-interfaces"></a>错误接口中的信息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  适用于 SQL Server 的 OLE DB 驱动程序在 OLE DB 定义的错误接口 IErrorInfo、IErrorRecords 和 ISQLErrorInfo 中报告某些错误和状态信息    。  
  
 适用于 SQL Server 的 OLE DB 驱动程序支持**IErrorInfo**成员函数，如下所示。  
  
|成员函数|描述|  
|---------------------|-----------------|  
|**GetDescription**|错误消息说明性字符串。|  
|**GetGUID**|定义错误的接口的 GUID。|  
|**GetHelpContext**|不提供支持。 始终返回零。|  
|**GetHelpFile**|不提供支持。 始终返回 NULL。|  
|**GetSource**|字符串“适用于 SQL Server 的 Microsoft OLE DB 驱动程序”。|  
  
 适用于 SQL Server 的 OLE DB 驱动程序支持使用者可用**IErrorRecords**成员函数，如下所示。  
  
|成员函数|描述|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|使用有关错误的基本信息填充 ERRORINFO 结构。 ERRORINFO 结构包含标识错误的 HRESULT 返回值的成员、访问接口和该错误适用的接口。|  
|**GetCustomErrorObject**|返回对 ISQLErrorInfo 和 [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 接口的引用  。|  
|**GetErrorInfo**|返回对 IErrorInfo 接口的引用  。|  
|**GetErrorParameters**|SQL Server 的 OLE DB 驱动程序不返回给使用者通过参数**GetErrorParameters**。|  
|**GetRecordCount**|可用错误记录的计数。|  
  
 适用于 SQL Server 的 OLE DB 驱动程序支持**isqlerrorinfo:: Getsqlinfo**参数，如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
|pbstrSQLState |返回错误的 SQLSTATE 值。 SQLSTATE 值在 SQL-92、ODBC 和 ISO SQL 以及 API 规范中定义。 既不[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]也适用于 SQL Server，OLE DB 驱动程序定义特定于实现的 SQLSTATE 值。|  
|plNativeError |返回 master.dbo.sysmessages 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 错误编号（如果存在）  。 在成功尝试初始化用于 SQL Server 数据源的 OLE DB 驱动程序后，本机错误将可用。 在之前尝试，SQL Server 的 OLE DB 驱动程序始终返回零。|  
  
## <a name="see-also"></a>另请参阅  
 [错误](../../oledb/ole-db-errors/errors.md)  
  
  
