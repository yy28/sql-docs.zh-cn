---
title: 表值参数 (OLE DB) |Microsoft Docs
description: 表值参数 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 6aa80999bcd7e4633aee7ae0a6aef30838896df6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628005"
---
# <a name="table-valued-parameters-ole-db"></a>表值参数 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本部分介绍 SQL Server 的 OLE DB 驱动程序中的表值参数的支持。 有关其他概述信息，请参阅[表值参数&#40;OLE DB 驱动程序适用于 SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)。 有关示例，请参阅[使用表值参数&#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)。  
  
## <a name="remarks"></a>Remarks  
 现在，可向服务器发送多行数据作为带参数集的过程的参数（如 ICommand::Execute 中的 DBPARAMS 参数）。 使用参数集时，该参数集中的每个元素都必须通过单独的远程过程调用 (RPC) 请求发送到服务器。 表值参数提供类似的功能，但可以与服务器更好地集成。 它减少了 RPC 请求数，并在服务器上启用基于集的操作。  
  
 作为 OLE DB 的 SQL Server 的 OLE DB 驱动程序中支持表值参数**行集**对象。 使用者（即使用适用于 SQL Server 的 OLE DB 驱动程序的客户端应用程序）可将任意 Rowset 对象提供用作表值参数的占位符。 表值参数的处理方式与其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 参数类型相似。 SQL Server 的 OLE DB 驱动程序提供了创建、 发现、 规范、 绑定和架构接口。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [创建表值参数行集](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [表值参数类型发现](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [执行包含表值参数的命令](../../oledb/ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [向表值参数中插入数据](../../oledb/ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [为 OLE DB 表值参数更改的架构行集](../../oledb/ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB 表值参数类型支持](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB 表值参数类型支持（方法）](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB 表值参数类型支持（属性）](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [使用表值参数 (OLE DB)](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
