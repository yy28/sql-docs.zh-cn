---
title: ISQLServerErrorInfo::GetErrorInfo (OLE DB) |Microsoft 文档
description: ISQLServerErrorInfo::GetErrorInfo (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
apitype: COM
helpviewer_keywords:
- GetErrorInfo method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 936924540c5c55f8e333a64d794e54af098f7279
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2018
ms.locfileid: "35690190"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  将指针返回到用于 SQL Server SSERRORINFO 结构包含的 OLE DB 驱动程序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]错误详细信息。  
  
 SQL Server 的 OLE DB 驱动程序定义**ISQLServerErrorInfo**错误接口。 此接口返回详细信息从[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]错误，包括其严重性和状态。  

  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT GetErrorInfo(  
   SSERRORINFO**ppSSErrorInfo,  
   OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>参数  
 *ppSSErrorInfo*[out 一个]  
 指向 SSERRORINFO 结构的指针。 如果该方法将失败，或者没有任何[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]与错误关联的信息，该提供程序不会分配任何内存，并确保*ppSSErrorInfo*参数为 null 指针上输出。  
  
 *ppErrorStrings*[out 一个]  
 指向 Unicode 字符串指针的指针。 如果该方法将失败，或者没有任何[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]与错误关联的信息，该提供程序不会分配任何内存，并确保*ppErrorStrings*参数为 null 指针上输出。 释放*ppErrorStrings*参数与**IMalloc::Free**方法释放返回的 SSERRORINFO 结构的三个单个字符串成员，如在块中分配内存。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_INVALIDARG  
 任一*ppSSErrorInfo*或*ppErrorStrings*自变量为 NULL。  
  
 E_OUTOFMEMORY  
 SQL Server 的 OLE DB 驱动程序无法分配足够的内存来完成该请求。  
  
## <a name="remarks"></a>Remarks  
 SQL Server 的 OLE DB 驱动程序为通过传递使用者的指针返回 SSERRORINFO 和 OLECHAR 字符串分配内存。 使用者必须释放此内存通过使用**IMalloc::Free**方法时它不再需要访问的错误数据。  
  
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
  
|成员|Description|  
|------------|-----------------|  
|*pwszMessage*|来自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的错误消息。 通过返回的消息 **:: Getdescription**方法。|  
|*pwszServer*|在其上发生了该错误的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。|  
|*pwszProcedure*|如果错误发生在存储过程中，则为生成该错误的存储过程的名称；否则，为空字符串。|  
|*lNative*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 错误号。 错误号等同于在中返回*plNativeError*参数**ISQLErrorInfo::GetSQLInfo**方法。|  
|*bState*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 错误的状态。|  
|*b 级 a*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 错误的严重性。|  
|*wLineNumber*|如果适用，为生成错误消息的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 存储过程的行。 如果与过程无关，则为默认值 1。|  
  
 结构中的指针引用中返回的字符串中的地址*ppErrorStrings*自变量。  
  
## <a name="see-also"></a>请参阅  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)   
 [RAISERROR (Transact-SQL)](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
