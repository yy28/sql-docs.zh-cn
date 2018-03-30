---
title: FILESTREAM 支持 (OLE DB) |Microsoft 文档
description: FILESTREAM 支持 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e7b1670cdda78f096ef776e7527910e71617c340
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="filestream-support-ole-db"></a>FILESTREAM 支持 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  开头[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和 OLE DB 驱动程序对于 SQL Server，OLE DB 支持增强的 FILESTREAM 功能。 有关此功能的详细信息，请参阅[FILESTREAM 支持](../../oledb/features/filestream-support.md)。 有关示例，请参阅[Filestream 和 OLE DB](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md)。  
  
 发送和接收**varbinary （max)**大于 2 GB 的值，应用程序使用**DBTYPE_IUNKNOWN**中参数和结果绑定。 参数的提供程序必须调用 iunknown:: Queryinterface ISequentialStream 和返回 ISequentialStream 的结果。  
  
 用于 OLE DB，检查相关为 ISequentialStream 值将通过放宽。 当*wType*是**DBTYPE_IUNKNOWN**中**DBBINDING**结构，检查长度可以是禁用通过省略**DBPART_LENGTH**从*dwPart*或通过设置数据的长度 (按偏移量*obLength*数据缓冲区中) 到 ~ 0。 在此情况下，提供程序将不检查值的长度，并且将请求和返回可通过流提供的所有数据。 这一更改将适用于所有大型对象 (LOB) 类型和 XML，但只在连接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]（或更高版本）服务器时才适用。 这将为开发人员提供更高的灵活性，同时为现有应用程序和下级服务器维护一致性和向下兼容性。  
  
 此更改影响所有传输数据，主要 irowset:: Getdata、 ICommand::Execute 和 IRowsetFastLoad::InsertRow 的接口。  
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 编程的 OLE DB 驱动程序](../../oledb/oledb-driver-for-sql-server-programming.md)  
  
  
