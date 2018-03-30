---
title: IBCPSession::BCPExec (OLE DB) |Microsoft 文档
description: IBCPSession::BCPExec (OLE DB)
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
- IBCPSession::BCPExec (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPExec method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8581d8a88598892f54643f38a907cd1e34d43b04
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="ibcpsessionbcpexec-ole-db"></a>IBCPSession::BCPExec (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  执行大容量复制操作。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPExec(   
      DBROWCOUNT *pRowsCopied);  
```  
  
## <a name="remarks"></a>注释  
 **BCPExec**方法复制将数据从用户文件到数据库表或者反之亦然，具体取决于值*eDirection*参数用于[IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)方法。  
  
 之前调用**BCPExec**，调用**BCPInit**具有有效的用户文件名称的方法。 如果没有这样做，会导致错误。 唯一的例外就是如果查询要用于大容量复制操作。 在这种情况下为中的表名称中指定 NULL **BCPInit**方法，然后指定使用 BCP_OPTION_HINTS 选项的查询。  
  
 **BCPExec**是唯一一种方法可能需要的任何时间长度内未完成的复制方法进行大容量。 因此，它是支持异步模式的唯一大容量复制方法。 若要使用异步模式，设置提供程序特定的会话属性 SSPROP_ASYNCH_BULKCOPY 为 VARIANT_TRUE，然后再调**BCPExec**方法。 此属性位于 DBPROPSET_SQLSERVERSESSION 属性集中。 若要测试是否完成，请调用**BCPExec**具有相同参数的方法。 如果大容量复制尚未完成， **BCPExec**方法返回 DB_S_ASYNCHRONOUS。 它还将在返回*pRowsCopied*参数状态的已发送到或从服务器收到的行数的计数。 发送到服务器的行直到到达批的末尾时才会提交。  
  
## <a name="arguments"></a>参数  
 *pRowsCopied*[out]  
 指向 DWORD 的指针。 **BCPExec**方法将 DWORD 填入成功复制的行数。 如果*pRowsCopied*自变量设置为 NULL，则将忽略该**BCPExec**方法。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 提供程序特定出错;详细信息，请使用[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)接口。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如， **BCPInit**方法未调用此方法之前调用。 如果该操作已中止通过使用 BCP_OPTION_ABORT 选项，也会发生与**BCPExec**之后调用了方法。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
 DB_S_ENDOFROWSET  
 大容量复制操作完成，所有数据传输已完成。  
  
 DB_S_ASYNCHRONOUS  
 当前这批行已复制。 调用**BCPExec**方法再次传输下一批。  
  
 DB_S_ERRORSOCCURRED  
 在大容量复制操作期间出现错误，可能尚未复制某些行。 错误数仍然小于允许的最大错误数。  
  
## <a name="see-also"></a>另请参阅  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [执行大容量复制操作](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
