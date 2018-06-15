---
title: 使用 OLE DB 驱动程序中的 OLE DB 中使用 OUTPUT 子句，用于 SQL Server |Microsoft 文档
description: 与 OLE DB 中 OLE DB 驱动程序中使用 OUTPUT 子句，用于 SQL Server
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8cf2e08b76636ab8509ab07fd1f3d60a102fa76d
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2018
ms.locfileid: "35665327"
---
# <a name="using-the-output-clause-with-ole-db-in-ole-db-driver-for-sql-server"></a>使用 OLE DB 驱动程序中的 OLE DB 中使用 OUTPUT 子句，用于 SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  如果你在 INSERT、 UPDATE、 DELETE 中使用 OUTPUT 子句，或合并命令，受影响的行计数不可用。 应用程序必须进行计数 OUTPUT 子句返回的行集中的行的数。  
  
## <a name="see-also"></a>请参阅  
 [创建适用于 SQL Server 的 OLE DB 驱动程序应用程序](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md) 
  
  
