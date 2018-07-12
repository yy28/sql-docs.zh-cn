---
title: 'Ibcpsession:: Bcpwritefmt (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IBCPSession::BCPWriteFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPWriteFmt method
ms.assetid: add50425-2ed6-411a-a391-4ce63c364892
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 68be3cd9b1296ed1f9e3530c4aadcc5a28cea891
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431046"
---
# <a name="ibcpsessionbcpwritefmt-ole-db"></a>IBCPSession::BCPWriteFmt (OLE DB)
  将每一列的格式信息写入格式化文件。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPWriteFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Remarks  
 格式化文件指定大容量复制所创建的数据文件的数据格式。 调用[ibcpsession:: Bcpcolumns](ibcpsession-bcpcolumns-ole-db.md)并[ibcpsession:: Bcpcolfmt](ibcpsession-bcpcolfmt-ole-db.md)方法定义的数据文件格式。 **BCPWriteFmt**方法将此定义保存在 pwszFormatFile 参数引用的文件中。  
  
 **BCPWriteFmt**方法可以 xml 或文本格式保存格式化文件。 这必须由使用 BCP_OPTION_XML 控制选项，用于指示[ibcpsession:: Bcpcontrol](ibcpsession-bcpcontrol-ole-db.md)方法。  
  
 若要加载已保存的格式化文件，请使用[ibcpsession:: Bcpreadfmt](ibcpsession-bcpreadfmt-ole-db.md)方法。  
  
## <a name="arguments"></a>参数  
 *pwszFormatFile*[in]  
 包含数据文件格式值的文件的路径和文件名。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 特定于访问接口时出错;详细信息，请使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)接口。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如， [ibcpsession:: Bcpinit](ibcpsession-bcpinit-ole-db.md)调用此方法之前，未调用方法。  
  
## <a name="see-also"></a>请参阅  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [执行大容量复制操作](../native-client/features/performing-bulk-copy-operations.md)  
  
  
