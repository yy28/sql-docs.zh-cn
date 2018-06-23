---
title: ISSAbort::Abort (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 41ddbfad313021431b409aa5054dc9afd18348b6
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35699938"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  取消当前行集以及与当前命令关联的任何批处理命令。  
  
**ISSAbort**接口，在中公开[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序提供**ISSAbort::Abort**批处理用于取消当前的行集加上任何命令的方法使用命令，最初生成行集，并且不具有尚未完成执行。  
  
 **ISSAbort**是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可通过使用本机客户端提供程序特定接口**QueryInterface**上**IMultipleResults**返回对象**ICommand::Execute**或**IOpenRowset::OpenRowset**。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Remarks  
 如果要中止的命令位于存储过程中，则将终止存储过程（以及已调用该过程的任何过程）以及包含此存储过程调用的命令批处理的执行。 如果服务器正在将结果集传输到客户端，则将停止此过程。 如果客户端不希望使用结果集，则调用**ISSAbort::Abort**释放行集将加快行集版本中，但如果没有打开的事务，且 XACT_ABORT 为 ON，将回滚事务之前当**ISSAbort::Abort**称为  
  
 后**ISSAbort::Abort**返回 S_OK，关联**IMultipleResults**接口进入不可用状态，并为所有方法调用返回 DB_E_CANCELED (除所定义的方法之外**IUnknown**接口) 之前它将被释放。 如果**IRowset**必须从获取**IMultipleResults**之前调用**中止**，它还进入不可用状态，并且返回 DB_E_CANCELED 到所有方法调用 （除由定义的方法之外**IUnknown**接口和**irowset:: Releaserows**) 之前它将被释放后成功调用**ISSAbort::Abort**.  
  
> [!NOTE]  
>  开头[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，如果服务器 XACT_ABORT 状态处于打开状态，执行**ISSAbort::Abort**将终止并回滚任何当前的隐式或显式事务，以连接到时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的较早版本不中止当前事务。  
  
## <a name="arguments"></a>参数  
 无。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 **ISSAbort::Abort**方法否则，返回批处理已取消的情况，则为 S_OK 和 DB_E_CANTCANCEL。 如果已经取消了批处理，则返回 DB_E_CANCELED。  
  
 DB_E_CANCELED  
 已经取消批处理。  
  
 DB_E_CANTCANCEL  
 批处理未取消。  
  
 E_FAIL  
 提供程序特定错误的发生;详细信息，请使用[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)接口。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如，对象处于僵停状态因为**ISSAbort::Abort**已调用。  
  
 E_OUTOFMEMORY  
 内存不足的错误。  
  
## <a name="see-also"></a>请参阅  
 [ISSAbort &#40;OLE DB&#41;](http://msdn.microsoft.com/library/7c4df482-4a83-4da0-802b-3637b507693a)  
  
  
