---
title: SQL Server 错误详细信息 |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b4b70a652ace8f7ccaf89ed23434ebed15410102
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35701988"
---
# <a name="sql-server-error-detail"></a>SQL Server 错误详细信息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序定义的提供程序特定的错误接口[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)。 该接口返回有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的更多详细信息，在命令执行或行集操作失败时这些信息很有用。  
  
 有两种方法来访问**ISQLServerErrorInfo**接口。  
  
 使用者都可以调用**IErrorRecords::GetCustomerErrorObject**获取**ISQLServerErrorInfo**指针，如下面的代码示例中所示。 (无需获取**ISQLErrorInfo。**)同时**ISQLErrorInfo**和**ISQLServerErrorInfo**是自定义 OLE DB 错误对象，而与**ISQLServerErrorInfo**正在使用来获取的信息的接口服务器错误，包括过程名称和行号等详细信息。  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 另一种方法来获取**ISQLServerErrorInfo**指针是调用**QueryInterface**方法已获取**ISQLErrorInfo**指针。 请注意，因为**ISQLServerErrorInfo**包含从可用信息的一个超集**ISQLErrorInfo**，因此若要直接转到**ISQLServerErrorInfo**通过**GetCustomerErrorObject**。  
  
 **ISQLServerErrorInfo**接口公开一个成员函数， [ISQLServerErrorInfo::GetErrorInfo](../../relational-databases/native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md)。 该函数返回 SSERRORINFO 结构的指针和字符串缓冲区的指针。 这两个指针引用使用者必须释放使用的内存**IMalloc::Free**方法。  
  
 SSERRORINFO 结构成员由使用者解释如下。  
  
|成员|Description|  
|------------|-----------------|  
|*pwszMessage*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误消息。 在返回的字符串相同 **:: Getdescription**。|  
|*pwszServer*|会话的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
|*pwszProcedure*|如果适用，则为产生错误的过程的名称。 否则为空字符串。|  
|*lNative*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机错误号。 返回的值与相同*plNativeError*参数**ISQLErrorInfo::GetSQLInfo**。|  
|*bState*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误消息的状态。|  
|*b 级 a*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误消息的严重性。|  
|*wLineNumber*|如果适用，则为发生错误的存储过程的行号。|  
  
## <a name="see-also"></a>请参阅  
 [错误](../../relational-databases/native-client-ole-db-errors/errors.md)   
 [RAISERROR (Transact-SQL)](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
