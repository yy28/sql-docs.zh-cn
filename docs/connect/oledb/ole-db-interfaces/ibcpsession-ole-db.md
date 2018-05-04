---
title: IBCPSession (OLE DB) |Microsoft 文档
description: IBCPSession 接口 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IBCPSession interface
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: fa5b620c5f8333ff54a046055e90867cedbfa87b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **IBCPSession**接口公开支持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]基于文件的大容量复制操作。 **IBCPSession**接口将公开 OLE DB 驱动程序中的 SQL Server 在与会话相同的级别下。 OLE DB 驱动程序中的 SQL Server，数据源对象是工厂对于会话对象，并在连接属性 SSPROP_ENABLEBULKCOPY 中指定大容量复制操作。 此外，SSPROP_ENABLEFASTLOAD 属性应当设置为 True。  
  
 调用**IDBCreateSession::CreateSession**方法然后将导致创建**BulkCopySession**对象。 通过公开的所有基于文件的大容量复制方法**IBCPSession**对象会使用对此几乎类似签名可调用**IBCPSession**对象的**IBCPSession**接口。  
  
> [!NOTE]  
>  SQL Server 的 OLE DB 驱动程序支持通过基于内存的大容量复制操作[IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)接口。  
  
 有关使用用于 SQL Server 的 OLE DB 驱动程序，大容量复制操作的详细信息，请参阅[执行大容量复制操作](../../oledb/features/performing-bulk-copy-operations.md)。  
  
 有关示例用于演示如何使用**IBCPSession**接口，请参阅[IBCPSession::BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|方法|Description|  
|------------|-----------------|  
|[IBCPSession::BCPColFmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)|在程序变量与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 列之间创建绑定。|  
|[IBCPSession::BCPColumns &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)|设置绑定到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表中列的字段数。|  
|[IBCPSession::BCPControl &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)|设置大容量复制操作的选项。|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)|提交要发送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的剩余行。|  
|[IBCPSession::BCPExec &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)|执行大容量复制操作。|  
|[IBCPSession::BCPInit &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)|初始化大容量复制结构，执行某些错误检查，验证数据和格式化文件名是否正确，然后打开文件。|  
|[IBCPSession::BCPReadFmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)|从格式化文件中读取每一列的格式信息。|  
|[IBCPSession::BCPWriteFmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)|将每一列的格式信息写入格式化文件。|  
  
## <a name="see-also"></a>另请参阅  
 [接口 & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)  
  
  
