---
title: 'Ibcpsession:: Bcpreadfmt (OLE DB) |Microsoft Docs'
description: '使用 ibcpsession:: Bcpreadfmt 从格式化文件 (OLE DB) 读取数据'
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPReadFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPReadFmt method
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 46139cddfb91c974f78547794bec55251abce25c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66790830"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  从格式化文件中读取每一列的格式信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPReadFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Remarks  
 可使用 BCPReadFmt 方法从格式化文件中读取数据，其中该文件指定数据文件中的数据格式  。 此方法能够检测格式化文件的正确版本。 它可以自动检测格式化文件采用的是 xml 格式还是旧式的文本格式，并据此执行操作。 为 SQL Server BCP 支持的 OLE DB 驱动程序的格式化文件版本是版本 6.0 或更高版本。  
  
 BCPReadFmt 方法在读取格式值之后，会相应调用 [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) 和 [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) 方法  。 用户不必分析格式化文件并发出上述调用。  
  
 要保存格式化文件，请调用 [IBCPSession::BCPWriteFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) 方法。 调用 BCPReadFmt 方法可引用保存的格式  。 或者，可使用大容量复制实用工具 (bcp) 将用户定义数据格式保存在可由 BCPReadFmt 方法引用的文件中   。  
  
 **BCP_OPTION_DELAYREADFMT**的值*eOption*参数[ibcpsession:: Bcpcontrol](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)修改 ibcpsession:: Bcpreadfmt 的行为。  
  
## <a name="arguments"></a>参数  
 pwszFormatFile  [in]  
 包含数据文件格式值的文件的路径和文件名。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 出现访问接口特定的错误；要获取详细信息，请使用 [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 接口。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如，在调用该方法之前，未调用 [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) 方法。  
  
## <a name="see-also"></a>另请参阅  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [执行大容量复制操作](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
