---
title: 'Issabort:: Abort (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fb9e2731c16773606f0b045ca004d520348e34b5
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43072070"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  取消当前行集以及与当前命令关联的任何批处理命令。  
  
**ISSAbort**接口中公开[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序提供**issabort:: Abort**用于取消当前行集以及任何命令的方法进行批处理使用命令的最初生成该行集，并且，尚未完成执行。  
  
 **ISSAbort**是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过使用提供的本机客户端特定于提供程序的界面**QueryInterface**上**IMultipleResults**返回的对象**Icommand:: Execute**或**iopenrowset:: Openrowset**。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Remarks  
 如果要中止的命令位于存储过程中，则将终止存储过程（以及已调用该过程的任何过程）以及包含此存储过程调用的命令批处理的执行。 如果服务器正在将结果集传输到客户端，则将停止此过程。 如果客户端不希望使用结果集，则在释放行集之前调用 ISSAbort::Abort 将加快行集释放，但是，如果存在打开的事务且 XACT_ABORT 为 ON，则当调用 ISSAbort::Abort 时，将回滚此事务  
  
 之后**issabort:: Abort**返回 S_OK 后，关联**IMultipleResults**接口进入不可用状态和所有方法调用都返回 DB_E_CANCELED (由定义的方法除外**IUnknown**接口) 发布后。 如果在调用 Abort 之前已从 IMultipleResults 获取了 IRowset，则它也会进入不可用状态，并对所有方法调用返回 DB_E_CANCELED（由 IUnknown 接口和 IRowset::ReleaseRows 定义的方法除外），直到在成功调用 ISSAbort::Abort 之后释放它为止。  
  
> [!NOTE]  
>  从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，如果服务器 XACT_ABORT 状态为 ON，则当连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，ISSAbort::Abort 的执行将终止并回滚当前所有的隐式或显式事务。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的较早版本不中止当前事务。  
  
## <a name="arguments"></a>参数  
 无。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 如果取消批处理，则 ISSAbort::Abort 方法返回 S_OK，否则返回 DB_E_CANTCANCEL。 如果已经取消了批处理，则返回 DB_E_CANCELED。  
  
 DB_E_CANCELED  
 已经取消批处理。  
  
 DB_E_CANTCANCEL  
 批处理未取消。  
  
 E_FAIL  
 提供程序特定错误出现则详细信息，请使用[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)接口。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如，因为已调用 ISSAbort::Abort，所以对象处于僵停状态。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
## <a name="see-also"></a>请参阅  
 [ISSAbort &#40;OLE DB&#41;](http://msdn.microsoft.com/library/7c4df482-4a83-4da0-802b-3637b507693a)  
  
  
