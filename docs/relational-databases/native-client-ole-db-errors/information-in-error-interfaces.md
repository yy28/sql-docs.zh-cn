---
title: 错误接口中的信息 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
ms.assetid: 4620f03f-1193-43e7-ba19-ad022737d300
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a19a2189aa28bb5ebf50a0533ed4bfb30b52deea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306082"
---
# <a name="information-in-error-interfaces"></a>错误接口中的信息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE DB 提供程序在 OLE DB 定义的错误接口**IErrorInfo、IError****记录**和**ISQLErrorInfo**中报告一些错误和状态信息。  
  
 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序支持**IErrorInfo**成员函数，如下所示。  
  
|成员函数|描述|  
|---------------------|-----------------|  
|**获取描述**|错误消息说明性字符串。|  
|**获取GUID**|定义错误的接口的 GUID。|  
|**GetHelpContext**|不支持。 始终返回零。|  
|**GetHelpFile**|不支持。 始终返回 NULL。|  
|**GetSource**|“Microsoft SQL Server Native Client”字符串。|  
  
 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序支持使用者可用的**IErrorRecords**成员函数，如下所示。  
  
|成员函数|描述|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|使用有关错误的基本信息填充 ERRORINFO 结构。 ERRORINFO 结构包含标识错误的 HRESULT 返回值的成员、访问接口和该错误适用的接口。|  
|**GetCustomErrorObject**|返回对 ISQLErrorInfo 和 [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 接口的引用****。|  
|**GetErrorInfo**|返回对 IErrorInfo 接口的引用****。|  
|**GetErrorParameters**|本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序不会通过**GetError 参数**向使用者返回参数。|  
|**GetRecordCount**|可用错误记录的计数。|  
  
 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序支持**ISQLErrorInfo：getSQLInfo**参数，如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
|pbstrSQLState**|返回错误的 SQLSTATE 值。 SQLSTATE 值在 SQL-92、ODBC 和 ISO SQL 以及 API 规范中定义。 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]OLE 数据库提供程序均未定义特定于实现的 SQLSTATE 值。|  
|plNativeError**|返回 master.dbo.sysmessages 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误编号（如果存在）****。 成功尝试初始化[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序数据源后，本机错误可用。 在尝试之前，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序始终返回零。|  
  
## <a name="see-also"></a>另请参阅  
 [错误](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
