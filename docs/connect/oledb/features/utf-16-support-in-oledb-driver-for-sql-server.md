---
title: OLE DB Driver for SQL Server 中的 UTF-16 支持 | Microsoft Docs
description: 适用于 SQL Server 的 OLE DB 驱动程序中的 UTF-16 支持
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: e0c76b7a62150fe4ee53fd83b63d7b9ebe1fd737
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47641707"
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 OLE DB 驱动程序中的 UTF-16 支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  自 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 起，如果出现下列情况，适用于 SQL Server 的 OLE DB 驱动程序将不向缓冲区添加高代理项码位：如果在绑定列结果或输出参数时提供了长度固定的缓冲区，如果在缓冲区中终止符前面写入的 wchar 字符是代理项对的高代理项码位，以及如果下一个 wchar 字符是一个低代理项码位。  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序功能](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
