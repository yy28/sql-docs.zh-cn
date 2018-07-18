---
title: 'Ibcpsession:: Bcpreadfmt (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IBCPSession::BCPReadFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPReadFmt method
ms.assetid: e2a12050-94e4-48a3-8a48-b780d646f116
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aa0f1501955db61889bb437e545cda95dfe8b31f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428249"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
  从格式化文件中读取每一列的格式信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPReadFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Remarks  
 **BCPReadFmt**方法用于从数据文件中指定的数据格式的格式文件中读取数据。 此方法能够检测格式化文件的正确版本。 它可以自动检测格式化文件采用的是 xml 格式还是旧式的文本格式，并据此执行操作。 支持的格式文件版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口 BCP 是 6.0 或更高版本。  
  
 之后**BCPReadFmt**方法读取格式值，它就会相应调用[ibcpsession:: Bcpcolumns](ibcpsession-bcpcolumns-ole-db.md)并[ibcpsession:: Bcpcolfmt](ibcpsession-bcpcolfmt-ole-db.md)方法。 用户不必分析格式化文件并发出上述调用。  
  
 若要保存格式化文件，请调用[ibcpsession:: Bcpwritefmt](ibcpsession-bcpwritefmt-ole-db.md)方法。 调用**BCPReadFmt**方法可以引用保存的格式。 或者，使用大容量复制实用工具 (**bcp**) 可以将用户定义数据格式保存在可以引用的文件**BCPReadFmt**方法。  
  
 `BCP_OPTION_DELAYREADFMT`的值*eOption*参数[ibcpsession:: Bcpcontrol](ibcpsession-bcpcontrol-ole-db.md)修改 ibcpsession:: Bcpreadfmt 的行为。  
  
## <a name="arguments"></a>参数  
 *pwszFormatFile*[in]  
 包含数据文件格式值的文件的路径和文件名。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 有关详细的信息可使用特定于提供程序的错误发生[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)接口。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如， [ibcpsession:: Bcpinit](ibcpsession-bcpinit-ole-db.md)调用此方法之前，未调用方法。  
  
## <a name="see-also"></a>请参阅  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [执行大容量复制操作](../native-client/features/performing-bulk-copy-operations.md)  
  
  
