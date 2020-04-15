---
title: ISSAbort::Abort (OLE DB) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8ce2c92dad8c0ff97cdbcf4e77a58e8dd6ceb18c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303978"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  取消当前行集以及与当前命令关联的任何批处理命令。  
  
**ISSAbort**接口在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序中公开，它提供**ISSAbort：：abort**方法，该方法用于取消当前行集以及使用最初生成行集的命令批处理且尚未完成执行的命令生成的任何命令。  
  
 **ISSAbort**是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一个本机客户端提供程序特定的接口，可通过在**ICommand：执行**或**IOpenRowset：：OpenRowset**返回的**IMulti结果**对象上使用**查询接口**可用。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>备注  
 如果要中止的命令位于存储过程中，则将终止存储过程（以及已调用该过程的任何过程）以及包含此存储过程调用的命令批处理的执行。 如果服务器正在将结果集传输到客户端，则将停止此过程。 如果客户端不希望使用结果集，则在释放行集之前调用 ISSAbort::Abort 将加快行集释放，但是，如果存在打开的事务且 XACT_ABORT 为 ON，则当调用 ISSAbort::Abort 时，将回滚此事务********  
  
 **在 ISSAbort：：abort**返回S_OK后，关联的**IMulti结果**接口将进入不可用状态，并返回DB_E_CANCELED所有方法调用 **（I未知**接口定义的方法除外），直到释放它。 如果在调用 Abort 之前已从 IMultipleResults 获取了 IRowset，则它也会进入不可用状态，并对所有方法调用返回 DB_E_CANCELED（由 IUnknown 接口和 IRowset::ReleaseRows 定义的方法除外），直到在成功调用 ISSAbort::Abort 之后释放它为止************************。  
  
> [!NOTE]  
>  从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，如果服务器 XACT_ABORT 状态为 ON，则当连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，ISSAbort::Abort 的执行将终止并回滚当前所有的隐式或显式事务****。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的较早版本不中止当前事务。  
  
## <a name="arguments"></a>参数  
 无。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 如果取消批处理，则 ISSAbort::Abort 方法返回 S_OK，否则返回 DB_E_CANTCANCEL****。 如果已经取消了批处理，则返回 DB_E_CANCELED。  
  
 DB_E_CANCELED  
 已经取消批处理。  
  
 DB_E_CANTCANCEL  
 批处理未取消。  
  
 E_FAIL  
 发生提供程序特定错误;有关详细信息，请使用[ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)界面。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如，因为已调用 ISSAbort::Abort，所以对象处于僵停状态****。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
## <a name="see-also"></a>另请参阅  
 [ISSAbort &#40;OLE DB&#41;](https://msdn.microsoft.com/library/7c4df482-4a83-4da0-802b-3637b507693a)  
  
  
