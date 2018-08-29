---
title: 将 OUTPUT 子句与适用于 SQL Server 的 OLE DB 驱动程序中的 OLE DB 结合使用 | Microsoft Docs
description: 将 OUTPUT 子句与适用于 SQL Server 的 OLE DB 驱动程序中的 OLE DB 结合使用
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: f559ff4169cda9d7740efc48499153332cb6de33
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43026366"
---
# <a name="using-the-output-clause-with-ole-db-in-ole-db-driver-for-sql-server"></a>将 OUTPUT 子句与适用于 SQL Server 的 OLE DB 驱动程序中的 OLE DB 结合使用
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  如果在 INSERT、UPDATE、DELETE 或 MERGE 命令中使用 OUTPUT 子句，则无法获得受影响的行数。 应用程序必须对 OUTPUT 子句所返回的行集中的行数进行计数。  
  
## <a name="see-also"></a>另请参阅  
 [创建适用于 SQL Server 的 OLE DB 驱动程序应用程序](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md) 
  
  
