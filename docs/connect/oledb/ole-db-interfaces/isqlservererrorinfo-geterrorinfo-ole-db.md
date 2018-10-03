---
title: 'Isqlservererrorinfo:: Geterrorinfo (OLE DB) |Microsoft Docs'
description: ISQLServerErrorInfo::GetErrorInfo (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
apitype: COM
helpviewer_keywords:
- GetErrorInfo method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: ce85539caa2c364a2ae8459fef0971c6cf2c2a54
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774339"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  返回一个指向用于 SQL Server SSERRORINFO 结构包含一个 OLE DB 驱动程序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]错误详细信息。  
  
 SQL Server 的 OLE DB 驱动程序定义**ISQLServerErrorInfo**错误接口。 此接口从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 错误返回详细信息，包括其严重性和状态。  

  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT GetErrorInfo(  
   SSERRORINFO**ppSSErrorInfo,  
   OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>参数  
 ppSSErrorInfo[out]  
 指向 SSERRORINFO 结构的指针。 如果方法失败或者不存在与该错误关联的任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 信息，则访问接口不会分配任何内存，并且会确保 ppSSErrorInfo 参数在输出时为一个空指针。  
  
 ppErrorStrings[out]  
 指向 Unicode 字符串指针的指针。 如果方法失败或者不存在与该错误关联的任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 信息，则访问接口不会分配任何内存，并且会确保 ppErrorStrings 参数在输出时为一个空指针。 如果使用 IMalloc::Free 方法释放 ppErrorStrings 参数，则会释放所返回的 SSERRORINFO 结构的三个单个字符串成员，因为内存是按块进行分配的。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_INVALIDARG  
 任一*ppSSErrorInfo*或*ppErrorStrings*参数为 NULL。  
  
 E_OUTOFMEMORY  
 SQL Server 的 OLE DB 驱动程序无法分配足够的内存来完成该请求。  
  
## <a name="remarks"></a>Remarks  
 适用于 SQL Server 的 OLE DB 驱动程序为通过使用者传递的指针返回的 SSERRORINFO 和 OLECHAR 字符串分配内存。 当使用者不再需要访问错误数据时，使用者必须使用 IMalloc::Free 方法释放该内存。  
  
 SSERRORINFO 结构的定义如下所示：  
  
```  
typedef struct tagSSErrorInfo  
   {  
   LPOLESTR pwszMessage;  
   LPOLESTR pwszServer;  
   LPOLESTR pwszProcedure;  
   LONG lNative;  
   BYTE bState;  
   BYTE bClass;  
   WORD wLineNumber;  
   }  
SSERRORINFO;  
```  
  
|成员|描述|  
|------------|-----------------|  
|pwszMessage|来自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的错误消息。 消息是通过 IErrorInfo::GetDescription 方法返回的。|  
|pwszServer|在其上发生了该错误的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。|  
|pwszProcedure|如果错误发生在存储过程中，则为生成该错误的存储过程的名称；否则，为空字符串。|  
|lNative|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 错误号。 该错误号与在 ISQLErrorInfo::GetSQLInfo 方法的 plNativeError 参数中返回的错误号相同。|  
|bState|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 错误的状态。|  
|bClass|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 错误的严重性。|  
|wLineNumber|如果适用，为生成错误消息的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 存储过程的行。 如果与过程无关，则为默认值 1。|  
  
 结构中的指针引用在 ppErrorStrings 参数中返回的字符串中的地址。  
  
## <a name="see-also"></a>另请参阅  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)   
 [RAISERROR (Transact-SQL)](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
