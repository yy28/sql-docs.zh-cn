---
title: SQL Server 错误详细信息 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
ms.assetid: 51500ee3-3d78-47ec-b90f-ebfc55642e06
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b937fda454ae08549917cdf3682ef20c76373a6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408986"
---
# <a name="sql-server-error-detail"></a>SQL Server 错误详细信息
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序定义的特定于提供程序的错误接口[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)。 该接口返回有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的更多详细信息，在命令执行或行集操作失败时这些信息很有用。  
  
 有两种方法要获得访问权限**ISQLServerErrorInfo**接口。  
  
 使用者可调用**ierrorrecords:: Getcustomererrorobject**来获取**ISQLServerErrorInfo**指针，如下面的代码示例中所示。 (若要获取无需**ISQLErrorInfo。**)这两**ISQLErrorInfo**并**ISQLServerErrorInfo**以自定义 OLE DB 错误对象**ISQLServerErrorInfo**所要使用获取的信息的接口服务器错误，包括诸如过程名称和行号的详细。  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 另一种方法获取**ISQLServerErrorInfo**指针是调用**QueryInterface**方法已经获得**ISQLErrorInfo**指针。 请注意，由于**ISQLServerErrorInfo**包含的信息可从超集**ISQLErrorInfo**，最好直接转到**ISQLServerErrorInfo**通过**GetCustomerErrorObject**。  
  
 **ISQLServerErrorInfo**接口公开一个成员函数[isqlservererrorinfo:: Geterrorinfo](../native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md)。 该函数返回 SSERRORINFO 结构的指针和字符串缓冲区的指针。 这两个指针引用使用者必须通过使用解除分配的内存**imalloc:: Free**方法。  
  
 SSERRORINFO 结构成员由使用者解释如下。  
  
|成员|Description|  
|------------|-----------------|  
|*pwszMessage*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误消息。 在中返回的字符串相同**ierrorinfo:: Getdescription**。|  
|*pwszServer*|会话的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
|*pwszProcedure*|如果适用，则为产生错误的过程的名称。 否则为空字符串。|  
|*lNative*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机错误号。 在中返回的值相同*plNativeError*的参数**isqlerrorinfo:: Getsqlinfo**。|  
|*bState*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误消息的状态。|  
|*bClass*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误消息的严重性。|  
|*wLineNumber*|如果适用，则为发生错误的存储过程的行号。|  
  
## <a name="see-also"></a>请参阅  
 [错误](errors.md)   
 [RAISERROR (Transact-SQL)](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  
