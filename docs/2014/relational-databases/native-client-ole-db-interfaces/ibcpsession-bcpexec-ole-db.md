---
title: 'Ibcpsession:: Bcpexec (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IBCPSession::BCPExec (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPExec method
ms.assetid: 0f4ebb63-cf03-4e53-846e-6c3021cde007
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb0c10e4c12bba99225bc5f332a8ad6701de29fd
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414026"
---
# <a name="ibcpsessionbcpexec-ole-db"></a>IBCPSession::BCPExec (OLE DB)
  执行大容量复制操作。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPExec(   
DBROWCOUNT *pRowsCopied);  
```  
  
## <a name="remarks"></a>Remarks  
 **BCPExec**方法复制将数据从用户文件到数据库表，反之亦然，具体取决于值*eDirection*参数用于[ibcpsession:: Bcpinit](ibcpsession-bcpinit-ole-db.md)方法。  
  
 然后再调用**BCPExec**，调用**BCPInit**具有有效的用户文件名称的方法。 如果没有这样做，会导致错误。 唯一的例外就是如果查询要用于大容量复制操作。 在这种情况下为中的表名称指定 NULL **BCPInit**方法，然后指定使用 BCP_OPTION_HINTS 选项的查询。  
  
 **BCPExec**方法是唯一大容量复制方法是可能胜任任何时间长度。 因此，它是支持异步模式的唯一大容量复制方法。 若要使用异步模式下，设置提供程序特定的会话属性 ssprop_asynch_bulkcopy 设置为 VARIANT_TRUE，然后再调**BCPExec**方法。 此属性位于 DBPROPSET_SQLSERVERSESSION 属性集中。 若要测试的完成情况，请调用**BCPExec**使用相同的参数的方法。 如果大容量复制尚未完成， **BCPExec**方法会返回 DB_S_ASYNCHRONOUS。 它还会返回在*pRowsCopied*参数状态的已发送到或从服务器收到的行数的计数。 发送到服务器的行直到到达批的末尾时才会提交。  
  
## <a name="arguments"></a>参数  
 *pRowsCopied*[out]  
 指向 DWORD 的指针。 **BCPExec**方法用成功复制的行数填充 DWORD。 如果*pRowsCopied*参数设置为 NULL，则忽略了**BCPExec**方法。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 特定于访问接口时出错;详细信息，请使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)接口。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如， **BCPInit**调用此方法之前，未调用方法。 如果已通过使用 BCP_OPTION_ABORT 选项中止该操作也会发生并**BCPExec**之后调用了方法。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
 DB_S_ENDOFROWSET  
 大容量复制操作完成，所有数据传输已完成。  
  
 DB_S_ASYNCHRONOUS  
 当前这批行已复制。 调用**BCPExec**方法再次传输下一批。  
  
 DB_S_ERRORSOCCURRED  
 在大容量复制操作期间出现错误，可能尚未复制某些行。 错误数仍然小于允许的最大错误数。  
  
## <a name="see-also"></a>请参阅  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [执行大容量复制操作](../native-client/features/performing-bulk-copy-operations.md)  
  
  
