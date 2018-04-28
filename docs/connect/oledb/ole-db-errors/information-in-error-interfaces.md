---
title: 错误接口中的信息 |Microsoft 文档
description: 错误接口中的信息
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 732dc76e63b1503aa0294a3381b53f592fbf25ce
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="information-in-error-interfaces"></a>错误接口中的信息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 的 OLE DB 驱动程序报告的 OLE DB 定义的错误接口中的某些错误和状态信息**IErrorInfo**， **IErrorRecords**，和**ISQLErrorInfo**。  
  
 SQL Server 的 OLE DB 驱动程序支持**IErrorInfo**成员函数，如下所示。  
  
|成员函数|Description|  
|---------------------|-----------------|  
|**GetDescription**|错误消息说明性字符串。|  
|**GetGUID**|定义错误的接口的 GUID。|  
|**GetHelpContext**|不提供支持。 始终返回零。|  
|**GetHelpFile**|不提供支持。 始终返回 NULL。|  
|**GetSource**|字符串"Microsoft OLE DB 驱动程序的 SQL Server"。|  
  
 SQL Server 的 OLE DB 驱动程序支持使用者可用**IErrorRecords**成员函数，如下所示。  
  
|成员函数|Description|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|使用有关错误的基本信息填充 ERRORINFO 结构。 ERRORINFO 结构包含标识错误的 HRESULT 返回值的成员、访问接口和该错误适用的接口。|  
|**GetCustomErrorObject**|在接口上返回的引用**ISQLErrorInfo，**和[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)。|  
|**GetErrorInfo**|在返回的引用**IErrorInfo**接口。|  
|**GetErrorParameters**|SQL Server 的 OLE DB 驱动程序不会返回使用者通过参数**GetErrorParameters**。|  
|**GetRecordCount**|可用错误记录的计数。|  
  
 SQL Server 的 OLE DB 驱动程序支持**ISQLErrorInfo::GetSQLInfo** ，如下所示的参数。  
  
|参数|Description|  
|---------------|-----------------|  
|*pbstrSQLState*|返回错误的 SQLSTATE 值。 SQLSTATE 值在 SQL-92、ODBC 和 ISO SQL 以及 API 规范中定义。 既不[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]也用于 SQL Server 的 OLE DB 驱动程序定义特定于实现的 SQLSTATE 值。|  
|*plNativeError*|返回[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]错误号**master.dbo.sysmessages**时可用。 初始化用于 SQL Server 数据源的 OLE DB 驱动程序是成功的尝试后提供本机错误。 之前尝试，SQL Server 的 OLE DB 驱动程序将始终返回零。|  
  
## <a name="see-also"></a>另请参阅  
 [错误](../../oledb/ole-db-errors/errors.md)  
  
  
