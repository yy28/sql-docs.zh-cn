---
title: IBCPSession：： BCPReadFmt （OLE DB） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPReadFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPReadFmt method
ms.assetid: e2a12050-94e4-48a3-8a48-b780d646f116
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a82cd2b9261b8f8c26e4e37636423cc27603fcc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63192409"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
  从格式化文件中读取每一列的格式信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPReadFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>备注  
 可使用 BCPReadFmt 方法从格式化文件中读取数据，其中该文件指定数据文件中的数据格式****。 此方法能够检测格式化文件的正确版本。 它可以自动检测格式化文件采用的是 xml 格式还是旧式的文本格式，并据此执行操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端支持的格式化文件版本 OLE DB 提供程序 BCP 为版本6.0 或更高版本。  
  
 BCPReadFmt 方法在读取格式值之后，会相应调用 **IBCPSession::BCPColumns** 和 [IBCPSession::BCPColFmt](ibcpsession-bcpcolumns-ole-db.md) 方法[](ibcpsession-bcpcolfmt-ole-db.md)。 用户不必分析格式化文件并发出上述调用。  
  
 要保存格式化文件，请调用 [IBCPSession::BCPWriteFmt](ibcpsession-bcpwritefmt-ole-db.md) 方法。 调用 BCPReadFmt 方法可引用保存的格式****。 或者，可使用大容量复制实用工具 (bcp) 将用户定义数据格式保存在可由 BCPReadFmt 方法引用的文件中********。  
  
 `BCP_OPTION_DELAYREADFMT` [IBCPSession：： BCPControl](ibcpsession-bcpcontrol-ole-db.md)的*eOption*参数的值修改了 IBCPSession：： BCPReadFmt 的行为。  
  
## <a name="arguments"></a>参数  
 *pwszFormatFile*[in]  
 包含数据文件格式值的文件的路径和文件名。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 出现特定于提供程序的错误，有关详细信息，请使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)接口。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如，在调用该方法之前，未调用 [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md) 方法。  
  
## <a name="see-also"></a>另请参阅  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [执行大容量复制操作](../native-client/features/performing-bulk-copy-operations.md)  
  
  
