---
title: 'Isqlservererrorinfo:: Geterrorinfo (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- GetErrorInfo method
ms.assetid: 83265c9c-eaf9-41f0-9f73-b0ae0972f0d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9131c65236a0efffa19aab2bd10b1fd8e309653b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127789"
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
 ppSSErrorInfo[out]  
 指向 SSERRORINFO 结构的指针。 如果方法失败或者不存在与该错误关联的任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 信息，则访问接口不会分配任何内存，并且会确保 ppSSErrorInfo 参数在输出时为一个空指针。  
  
 ppErrorStrings[out]  
 指向 Unicode 字符串指针的指针。 如果方法失败或者不存在与该错误关联的任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 信息，则访问接口不会分配任何内存，并且会确保 ppErrorStrings 参数在输出时为一个空指针。 如果使用 IMalloc::Free 方法释放 ppErrorStrings 参数，则会释放所返回的 SSERRORINFO 结构的三个单个字符串成员，因为内存是按块进行分配的。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_INVALIDARG  
 任一*ppSSErrorInfo*或*ppErrorStrings*参数为 NULL。  
  
 E_OUTOFMEMORY  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序无法分配足够的内存来完成该请求。  
  
## <a name="remarks"></a>备注  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口为由使用者传递的指针返回的 SSERRORINFO 和 OLECHAR 字符串分配内存。 当使用者不再需要访问错误数据时，使用者必须使用 IMalloc::Free 方法释放该内存。  
  
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
|pwszMessage|来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的错误消息。 消息是通过 IErrorInfo::GetDescription 方法返回的。|  
|pwszServer|在其上发生了该错误的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
|pwszProcedure|如果错误发生在存储过程中，则为生成该错误的存储过程的名称；否则，为空字符串。|  
|lNative|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误号。 该错误号与在 ISQLErrorInfo::GetSQLInfo 方法的 plNativeError 参数中返回的错误号相同。|  
|*bState*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的状态。|  
|bClass|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的严重性。|  
|wLineNumber|如果适用，为生成错误消息的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程的行。 如果与过程无关，则为默认值 1。|  
  
 结构中的指针引用在 ppErrorStrings 参数中返回的字符串中的地址。  
  
## <a name="see-also"></a>请参阅  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)   
 [RAISERROR (Transact-SQL)](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  
