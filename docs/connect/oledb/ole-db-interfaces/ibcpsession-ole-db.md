---
title: IBCPSession (OLE DB) |Microsoft Docs
description: IBCPSession 接口 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IBCPSession interface
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 96603d7dcb6215513d67d4db5d29f8a762d57ea8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47764917"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  IBCPSession 接口公开了对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 基于文件的大容量复制操作的支持。 **IBCPSession**接口公开 OLE DB 驱动程序中的 SQL Server 下与会话相同的级别。 在适用于 SQL Server 的 OLE DB 驱动程序中，数据源对象是会话对象的工厂，且大容量复制操作在连接属性 SSPROP_ENABLEBULKCOPY 中指定。 此外，SSPROP_ENABLEFASTLOAD 属性应当设置为 True。  
  
 调用 IDBCreateSession::CreateSession 方法随后将创建 BulkCopySession 对象。 然后，可针对此 IBCPSession 对象的 IBCPSession 接口，采用极为相似的签名来调用通过 IBCPSession 对象公开的所有基于文件的大容量复制方法。  
  
> [!NOTE]  
>  适用于 SQL Server 的 OLE DB 驱动程序支持通过 [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) 接口进行基于内存的大容量复制操作。  
  
 有关使用用于 SQL Server 的 OLE DB 驱动程序，大容量复制操作的详细信息，请参阅[执行大容量复制操作](../../oledb/features/performing-bulk-copy-operations.md)。  
  
 有关演示如何使用的示例**IBCPSession**接口，请参阅[IBCPSession::BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|方法|描述|  
|------------|-----------------|  
|[Ibcpsession:: Bcpcolfmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)|在程序变量与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 列之间创建绑定。|  
|[Ibcpsession:: Bcpcolumns &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)|设置绑定到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表中列的字段数。|  
|[Ibcpsession:: Bcpcontrol &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)|设置大容量复制操作的选项。|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)|提交要发送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的剩余行。|  
|[Ibcpsession:: Bcpexec &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)|执行大容量复制操作。|  
|[Ibcpsession:: Bcpinit &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)|初始化大容量复制结构，执行某些错误检查，验证数据和格式化文件名是否正确，然后打开文件。|  
|[Ibcpsession:: Bcpreadfmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)|从格式化文件中读取每一列的格式信息。|  
|[Ibcpsession:: Bcpwritefmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)|将每一列的格式信息写入格式化文件。|  
  
## <a name="see-also"></a>另请参阅  
 [接口&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)  
  
  
