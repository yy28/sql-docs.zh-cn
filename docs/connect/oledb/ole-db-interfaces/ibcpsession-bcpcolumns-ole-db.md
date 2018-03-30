---
title: IBCPSession::BCPColumns (OLE DB) |Microsoft 文档
description: IBCPSession::BCPColumns (OLE DB)
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
- IBCPSession::BCPColumns (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColumns method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3526779f5f69011a10863ee475f3ec475daadee1
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  设置绑定到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表中列的字段数。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPColumns(   
      DBCOUNTITEM nColumns);  
```  
  
## <a name="remarks"></a>注释  
 它在内部调用[IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)设置字段数据的默认值。 这些默认值从 SQL Server 列检索的信息与提供程序内部通过指定表名称时获得的[IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)。  
  
> [!NOTE]  
>  可以调用此方法后，才**BCPInit**已调用具有有效的文件名称。  
  
 只有在您要使用不同于默认设置的用户文件格式时，才应调用此方法。 有关默认的用户文件格式的说明的详细信息，请参阅**BCPInit**方法。  
  
 在调用**BCPColumns**方法时，必须调用**BCPColFmt**要完整地定义自定义文件格式的用户文件中的每列的方法。  
  
## <a name="arguments"></a>参数  
 *nColumns*[in]  
 用户文件中字段的总数。 即使你准备大容量复制数据从用户文件复制到 SQL Server 表，并不打算将所有字段中的用户文件的都复制，则仍必须设置*nColumns*给总数量的用户文件字段的自变量。 然后可通过指定已跳过的字段**BCPColFmt**。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 提供程序特定出错;详细信息，请使用[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)接口。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如， **BCPInit**方法未调用此方法之前调用。 在为某一大容量复制操作多次调用此方法时，也会发生这一意外调用。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
## <a name="see-also"></a>另请参阅  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [执行大容量复制操作](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
