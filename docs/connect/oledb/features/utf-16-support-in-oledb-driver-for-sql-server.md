---
title: OLE DB 驱动程序中的 SQL Server 的 utf-16 支持 |Microsoft 文档
description: OLE DB 驱动程序中的 SQL Server 的 utf-16 支持
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b304cb7a713143facc479821d9bf318c6c150a54
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>OLE DB 驱动程序中的 SQL Server 的 utf-16 支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  从[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，如果绑定列结果或输出参数时提供固定长度缓冲区，并且如果**wchar**之前终止字符是一个高代理项码位的写入到缓冲区的字符代理项对，并且如果下一步**wchar**字符是一个低代理项码位，OLE DB 驱动程序的 SQL Server 将不向缓冲区添加的高代理项码位。  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序功能](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
