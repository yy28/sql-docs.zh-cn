---
title: IBCPSession::BCPReadFmt (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f47369cb66f6695ca7a235beb72536ce34495bb5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138649"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
  从格式化文件中读取每一列的格式信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPReadFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Remarks  
 **BCPReadFmt**方法用于从数据文件中指定的数据的格式的格式化文件中读取数据。 此方法能够检测格式化文件的正确版本。 它可以自动检测格式化文件采用的是 xml 格式还是旧式的文本格式，并据此执行操作。 支持的格式文件版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序 BCP 是 6.0 或更高版本。  
  
 后**BCPReadFmt**方法读取的值设置格式，它使到适当的调用[IBCPSession::BCPColumns](ibcpsession-bcpcolumns-ole-db.md)和[IBCPSession::BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md)方法。 用户不必分析格式化文件并发出上述调用。  
  
 若要保存格式文件，请调用[IBCPSession::BCPWriteFmt](ibcpsession-bcpwritefmt-ole-db.md)方法。 调用**BCPReadFmt**方法可以引用已保存的格式。 或者，大容量复制实用工具 (**bcp**) 可以在可供引用的文件中保存用户定义数据格式**BCPReadFmt**方法。  
  
 `BCP_OPTION_DELAYREADFMT`值*eOption*参数[IBCPSession::BCPControl](ibcpsession-bcpcontrol-ole-db.md)修改 IBCPSession::BCPReadFmt 的行为。  
  
## <a name="arguments"></a>参数  
 *pwszFormatFile*[in]  
 包含数据文件格式值的文件的路径和文件名。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 提供程序特定错误发生，有关详细的信息的使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)接口。  
  
 E_OUTOFMEMORY  
 内存不足的错误。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如， [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md)方法未调用此方法之前调用。  
  
## <a name="see-also"></a>请参阅  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [执行大容量复制操作](../native-client/features/performing-bulk-copy-operations.md)  
  
  