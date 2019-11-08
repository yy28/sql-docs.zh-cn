---
title: ISSAbort：： Abort （OLE DB） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d66d37da3ba2de7f12cefb8f806c44d5dd967003
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73763178"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  取消当前行集以及与当前命令关联的任何批处理命令。  
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序中公开的**ISSAbort**接口提供**ISSAbort：： Abort**方法，该方法用于取消当前行集以及使用初始生成的命令进行批处理的任何命令尚未完成的行集。  
  
 **ISSAbort**是一种 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的特定于 Native Client 提供程序的接口，可通过对**ICommand：： Execute**或**IOpenRowset：： OpenRowset**返回的**IMultipleResults**对象使用**QueryInterface** 。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>注释  
 如果要中止的命令位于存储过程中，则将终止存储过程（以及已调用该过程的任何过程）以及包含此存储过程调用的命令批处理的执行。 如果服务器正在将结果集传输到客户端，则将停止此过程。 如果客户端不希望使用结果集，则在释放行集之前调用 ISSAbort::Abort 将加快行集释放，但是，如果存在打开的事务且 XACT_ABORT 为 ON，则当调用 ISSAbort::Abort 时，将回滚此事务  
  
 **ISSAbort：： Abort**返回 S_OK 后，关联的**IMultipleResults**接口将进入不可用状态，并将 DB_E_CANCELED 返回给所有方法调用（ **IUnknown**接口定义的方法除外），直到它被释放。 如果在调用 Abort 之前已从 IMultipleResults 获取了 IRowset，则它也会进入不可用状态，并对所有方法调用返回 DB_E_CANCELED（由 IUnknown 接口和 IRowset::ReleaseRows 定义的方法除外），直到在成功调用 ISSAbort::Abort 之后释放它为止。  
  
> [!NOTE]  
>  从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，如果服务器 XACT_ABORT 状态为 ON，则当连接到  **时，ISSAbort::Abort 的执行将终止并回滚当前所有的隐式或显式事务**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的较早版本不中止当前事务。  
  
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
 发生了特定于提供程序的错误;有关详细信息，请使用[ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)接口。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如，因为已调用 ISSAbort::Abort，所以对象处于僵停状态。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
## <a name="see-also"></a>另请参阅  
 [ISSAbort &#40;OLE DB&#41;](https://msdn.microsoft.com/library/7c4df482-4a83-4da0-802b-3637b507693a)  
  
  
