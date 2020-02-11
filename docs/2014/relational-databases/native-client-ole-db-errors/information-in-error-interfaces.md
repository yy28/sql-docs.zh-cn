---
title: 错误接口中的信息 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60b6b0387aea5475d74c314a10e4fa437fadc005
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62657657"
---
# <a name="information-in-error-interfaces"></a>错误接口中的信息
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序在 OLE DB 定义的错误接口**IErrorInfo**、 **IErrorRecords**和**ISQLErrorInfo**中报告一些错误和状态信息。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持**IErrorInfo**成员函数，如下所示。  
  
|成员函数|说明|  
|---------------------|-----------------|  
|**GetDescription**|错误消息说明性字符串。|  
|**GetGUID**|定义错误的接口的 GUID。|  
|**GetHelpContext**|不支持。 始终返回零。|  
|**GetHelpFile**|不支持。 始终返回 NULL。|  
|**GetSource**|“Microsoft SQL Server Native Client”字符串。|  
  
 Native Client OLE DB 提供程序支持使用者可用的 IErrorRecords 成员函数，如下所示。 **** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
|成员函数|说明|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|使用有关错误的基本信息填充 ERRORINFO 结构。 ERRORINFO 结构包含标识错误的 HRESULT 返回值的成员、访问接口和该错误适用的接口。|  
|**GetCustomErrorObject**|返回对 ISQLErrorInfo 和 **ISQLServerErrorInfo** 接口的引用[](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)。|  
|**GetErrorInfo**|返回对 IErrorInfo 接口的引用****。|  
|**GetErrorParameters**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不通过**GetErrorParameters**将参数返回给使用者。|  
|**GetRecordCount**|可用错误记录的计数。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持**ISQLErrorInfo：： GetSQLInfo**参数，如下所示。  
  
|参数|说明|  
|---------------|-----------------|  
|*pbstrSQLState*|返回错误的 SQLSTATE 值。 SQLSTATE 值在 SQL-92、ODBC 和 ISO SQL 以及 API 规范中定义。 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 都不 OLE DB 提供程序定义的特定于实现的 SQLSTATE 值。|  
|*plNativeError*|返回 master.dbo.sysmessages 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误编号（如果存在）****。 在成功初始化[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序数据源后，会提供本机错误。 尝试之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序始终返回零。|  
  
## <a name="see-also"></a>另请参阅  
 [错误](errors.md)  
  
  
