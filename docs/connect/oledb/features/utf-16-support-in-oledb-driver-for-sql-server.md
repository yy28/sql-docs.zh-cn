---
title: OLE DB 驱动程序中的 SQL Server 的 utf-16 支持 |Microsoft 文档
description: OLE DB 驱动程序中的 SQL Server 的 utf-16 支持
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f4e1103b25deb46d03ce26a79ba3649305c283d
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>OLE DB 驱动程序中的 SQL Server 的 utf-16 支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  从[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，如果绑定列结果或输出参数时提供固定长度缓冲区，并且如果**wchar**之前终止字符是一个高代理项码位的写入到缓冲区的字符代理项对，并且如果下一步**wchar**字符是一个低代理项码位，OLE DB 驱动程序的 SQL Server 将不向缓冲区添加的高代理项码位。  
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 功能的 OLE DB 驱动程序](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
