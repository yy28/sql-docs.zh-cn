---
title: 'Isqlservererrorinfo:: Geterrorinfo (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- GetErrorInfo method
ms.assetid: 83265c9c-eaf9-41f0-9f73-b0ae0972f0d5
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f33c66d8e521339573e56b78407f0bab67b4b43e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430096"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
  返回一个指向[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口 SSERRORINFO 结构包含[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]错误详细信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
   HRESULT GetErrorInfo(  
SSERRORINFO**ppSSErrorInfo,  
OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>参数  
 *ppSSErrorInfo*[out]  
 指向 SSERRORINFO 结构的指针。 如果方法失败或者没有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与错误关联的信息，该提供程序不会分配任何内存，并确保*ppSSErrorInfo*参数为 null 指针上输出。  
  
 *ppErrorStrings*[out]  
 指向 Unicode 字符串指针的指针。 如果方法失败或者没有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与错误关联的信息，该提供程序不会分配任何内存，并确保*ppErrorStrings*参数为 null 指针上输出。 释放*ppErrorStrings*自变量与**imalloc:: Free**方法释放所返回的 SSERRORINFO 结构的三个单个字符串成员，如在块中分配内存。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_INVALIDARG  
 任一*ppSSErrorInfo*或*ppErrorStrings*参数为 NULL。  
  
 E_OUTOFMEMORY  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序无法分配足够的内存来完成该请求。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口为由使用者传递的指针返回的 SSERRORINFO 和 OLECHAR 字符串分配内存。 使用者必须释放此内存通过使用**imalloc:: Free**方法时不再需要对错误数据的访问。  
  
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
|*pwszMessage*|来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的错误消息。 通过返回的消息**ierrorinfo:: Getdescription**方法。|  
|*pwszServer*|在其上发生了该错误的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
|*pwszProcedure*|如果错误发生在存储过程中，则为生成该错误的存储过程的名称；否则，为空字符串。|  
|*lNative*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误号。 错误号是中返回的相同*plNativeError*的参数**isqlerrorinfo:: Getsqlinfo**方法。|  
|*bState*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的状态。|  
|*bClass*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的严重性。|  
|*wLineNumber*|如果适用，为生成错误消息的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程的行。 如果与过程无关，则为默认值 1。|  
  
 结构中的指针引用中返回的字符串中的地址*ppErrorStrings*参数。  
  
## <a name="see-also"></a>请参阅  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)   
 [RAISERROR (Transact-SQL)](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  
