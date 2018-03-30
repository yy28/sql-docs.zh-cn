---
title: ISSAbort::Abort (OLE DB) |Microsoft 文档
description: ISSAbort::Abort (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 81792a3eefe5d29b63614c3be71562de8540a1fd
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  取消当前行集以及与当前命令关联的任何批处理命令。  
  
**ISSAbort**接口，SQL Server 的 OLE DB 驱动程序中公开，提供了**ISSAbort::Abort**用于取消当前的行集加上任何命令的方法使用命令批处理最初生成行集，并且不具有尚未完成执行。  
  
 **ISSAbort**是使用可用 SQL Server 特定接口的 OLE DB 驱动程序**QueryInterface**上**IMultipleResults**返回对象**ICommand::Execute**或**IOpenRowset::OpenRowset**。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>注释  
 如果正在中止该命令是在存储过程中，存储的过程 （以及任何已调用该过程的过程） 的执行将终止以及包含存储的过程调用的命令批处理。 如果服务器正在传输到客户端设置的结果是，将停止传输。 如果客户端不希望使用结果集，则调用**ISSAbort::Abort**释放行集将加快行集版本中，但如果没有打开的事务，且 XACT_ABORT 为 ON，将回滚事务之前当**ISSAbort::Abort**称为  
  
 后**ISSAbort::Abort**返回 S_OK，关联**IMultipleResults**接口进入不可用状态，并为所有方法调用返回 DB_E_CANCELED (除所定义的方法之外**IUnknown**接口) 之前它将被释放。 如果**IRowset**必须通过**IMultipleResults**之前调用**中止**，它还进入不可用状态，并为所有方法调用返回 DB_E_CANCELED (除由定义的方法之外**IUnknown**接口和**irowset:: Releaserows**) 之前它将被释放后成功调用**ISSAbort::Abort**。  
  
> [!NOTE]  
>  开头[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，如果服务器 XACT_ABORT 状态处于打开状态，执行**ISSAbort::Abort**将终止并回滚任何当前的隐式或显式事务，以连接到时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的较早版本不中止当前事务。  
  
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
 提供程序特定出错;详细信息，请使用[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)接口。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如，对象处于僵停状态因为**ISSAbort::Abort**已调用。  
  
 E_OUTOFMEMORY  
 内存不足的错误。  
  
  
